---
description: >-
  Using Sero to make a Provider Directory API request and searching for
  in-network specialists
---

# Humana Hematology Specialist Search

## Overview

{% hint style="info" %}
The complete source code for this example is available at [**example/humana-specialist-search**](https://github.com/Automate-Medical/sero/tree/master/example/humana-specialist-search).  Are you interested in accessing newly launched Provider Directory data? Contact [**founders@automatemedical.com**](mailto:founders@automatemedical.com)\*\*\*\*
{% endhint %}

This example demonstrates how to use Sero to access ****[**Provider Directory APIs**](../../book/build/provider-directory.md) from health plan payers such as Humana. Using publicly accessible FHIR APIs, we are able to identify in-network specialists \(a hematologist in our example\) available for a given Humana plan.

If you click play [▶️](https://emojipedia.org/play-button/) button in the [Replit](https://replit.com/@jdjkelly/Humana-Specialist-Search) below, you will see the full example running. An initial request is made to find Humana Insurance Plans. Subsequent requests made to identify eligible Hematologists for a given plan.

{% embed url="https://replit.com/@jdjkelly/Humana-Specialist-Search" caption="Click the green play button for the full example to run" %}

More information about Humana's API is available at [developers.humana.com](https://developers.humana.com/apis).

### Walkthrough

Sero implements an [Client ](../../sero-reference/fhir-client.md)that can make requests to ****[**FHIR APIs**](https://docs.sero.run/book/how-to-build-in-health/fhir). Provider Directories are a practical, real world example of life FHIR APIs in the wild. You can learn more about FHIR and Provider Directories in our [**How to build in health the easy way**](https://docs.sero.run/book/how-to-build-in-health/clinical-decision-support-hooks) ebook.

This code walkthrough will focus primarily on [humana.ts](https://github.com/Automate-Medical/sero/blob/master/example/humana-specialist-search/humana.ts), where we start by importing Sero and querying the Humana API.

#### Imports

We start by importing the `Client` module from Sero. We're also going to be using a library called `Chalk` to print information about our queries.

```typescript
import { Client } from "@sero.run/sero"
import chalk from "chalk";
import { Humana } from "./glossary.js"
const { log } = console;
```

#### Step 1: Find Humana's Insurance Plan

We start by initializing the Client with the `baseUrl` of the FHIR API and destructuring the operations we will use \(`searchType` and `read`\). Then, we make a search for Humana's `InsurancePlan` resources. We use `async` and call `next` because Sero generates yields paginated results for searches through an [iterator and a generator function](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-6.html).

```typescript
const { searchType, read } = Client("https://fhir.humana.com/api")

const planSearch = await searchType("InsurancePlan").next()
```

We identify an eligible plan, and find its network details - specifically searching for the medical/dental network identifier associated with the plan. We'll use this in step 2.

```typescript
const insurancePlan = planSearch.value?.entry?.find((bundleEntry) => {
  return bundleEntry.resource?.resourceType == "InsurancePlan"
})?.resource as fhir4.InsurancePlan

const { name, plan, network } = insurancePlan;

const { value: planId } = network?.find(n => {
  return n.identifier?.system == Humana.MedicalDentalNetwork
})?.identifier as fhir4.Identifier
```

#### Step 2: Find an In-Network Hematology Practitioner Role

Now, we need to search for Hematology specialists \(or any other kind we want\) who have available coverage under the plan network we identified in step 1. We do this by forming a query against `PractitionerRole`, which is a [FHIR Resource](https://www.hl7.org/fhir/practitionerrole.html) that defines specializations.

The first step here is to define our query. Sero's `searchType` operation accepts a object as a second argument and automatically URI encodes the values to generate the API request. We're using quotes around the `"speciality:text"` key because `:` cannot be used in a symbol.

```typescript
const hematologyQuery = {
  "specialty:text": "Hematology",
  _tag: `${Humana.MedicalDentalNetwork}|${planId}`,
  active: true
}
```

Then, we make the query. Again, we call `next()` to return the first page of results. From the results, we try to find an eligible `Practitioner` \(Hematologist\).

```typescript
const specialistSearch = await searchType("PractitionerRole", hematologyQuery).next()

const specialistRole = specialistSearch.value?.entry?.find((bundleEntry) => {
  return bundleEntry.resource?.resourceType == "PractitionerRole" && bundleEntry.resource.practitioner
})?.resource as fhir4.PractitionerRole
```

#### Step 3: Query the Hematologist

If we were able to identify a `Practitioner` in step 2, we can make a query to retrieve their individual information including NPI:

```typescript
const { practitioner } = specialistRole;
if (!practitioner?.reference) throw new Error("No practitioner matched that search")
let readPractitioner = await read(practitioner.reference) as fhir4.Practitioner
```

Finally, we use `chalk` to log our queries and the final result to console.

