---
description: 'Processing request data, and providing simple decision support with Sero'
---

# Prefetch and Context

## What we'll be building

In this section, we'll be building a CDS service that receives a request to display demographic information about a patient being viewed by the CDS client. The service will determine the last encounter date of the patient based on their encounter history, and suggest that an appointment be booked again if it has been too long since their last appointment. 

This service will also be invoked with the `patient-view` hook.

{% hint style="info" %}
You can find the complete source for this guide in the Sero project at [**example/cds-hooks-api-guide**](https://github.com/Automate-Medical/sero/tree/master/example/cds-hooks-api-guide)
{% endhint %}

## Prefetch and Context

In the previous example, the service we made didn't access the HTTP `request` body. Although this is not _necessary_ when responding to a request, services that compute useful recommendations need to access the **contextual** information in the request, and request more **FHIR** data if needed through **prefetch templates**. 

### Context

When we create a service that invokes one of the CDS Hooks \(`patient-view`, `appointment-book`, `encounter-start`, etc.\), the CDS client needs to provide important contextual information to the service for the service to work properly. This information is a pre-defined agreement specified by CDS Hooks that guarantees that this information will be provided to the service by the CDS client. 

For example, if we head over to the [specification](https://cds-hooks.org/hooks/patient-view/#context) for the `patient-view` hook, we can see that there are required keys that need to be provided to the CDS service upon a hook request. In this example, `userId` and `patientId` are required, and `encounterId` is optional. This is because to perform useful actions for this hook, the service needs to know the current patient whose record is being viewed and the user who is viewing the record. We _might_ need to know the identity of the current encounter, but for this example we won't.

In general, it is implied that the CDS client, as a consumer of a service, will send the required values to the service to which it is making a request. As developers of CDS services, we do not need to worry about providing any additional parameters for context. 

If needed, we could retrieve it from the request body \(although it is not required for this walkthrough\). 

```javascript
const handler = async (request) => {
    const contextData = request.context;
}
```

### Prefetch and prefetch template

What if we need additional information to serve complex requests? 

A [**prefetch template**](https://cds-hooks.org/specification/current/#prefetch-template) is an object containing FHIR queries that a service defines when it needs additional information from the CDS client. When present, the CDS client executes FHIR path queries and includes this FHIR data in the request body. 

For example, the CDS client only provides basic contextual information by default. For the `patient-view` hook, this is only the `userId` and `patientId`. If the service wanted to recommend guidance based on a patients present condition, we would use a [**prefetch token**](https://cds-hooks.org/specification/current/#prefetch-tokens), or a FHIR query, to fetch this information. Below is the prefetch token that would accomplish this.

```javascript
"patient": "Patient/{{context.patientId}}",
```

This is what the prefetch template would look like.

```javascript
"prefetch": {
    "patient": "Patient/{{context.patientId}}",
  }
```

To retrieve this prefetch data in the request body, we would assign it to a variable matching the name of the key associated with the query.

```javascript
const patient = request.prefetch.patient;
```

`patient` is now a FHIR patient resource. 

The context values the hook provides are used in the prefetch template. For the example above, the `patientId` context value is used to execute the FHIR query on the client. The hook specifies which context values can be used in prefetch tokens.

### Summary

When a CDS client makes a request to a service, it knows to send important contextual information to that service. This depends on the hook, but expect the client to send these values. 

If the service needs extra information from the client in order to perform a task, it provides a prefetch template when configuring the service. When a CDS client goes to make a request to the service, it knows to take the prefetch template, execute the FHIR path queries on its FHIR data source, and return a prefetch object whose keys match the keys of the request. It is common that context fields such as `context.patientId` will be needed to execute these searches - they can be accessed with the double-handlebars syntax, `{{context.patientId}}`. 

## The code

### Imports

In the `src` directory, create a folder called `prefetch-context`. `cd` into it and create the file `prefetch-context.js`.  Import the `Service` and `Class` classes like last time. 

```javascript
import { Service, Card } from "@sero.run/sero";
```

### Options

The service's configuration options will look roughly the same as the previous services, excluding the modified `title`and  `description`, and added `prefetch` template.

```javascript
const options = {
  id: "prefetch-context",
  title: "Patient view with last encounter.",
  hook: "patient-view",
  description:
    "A patient-view hook with patient and encounter prefetch template values. Presents patient info and last encounter information",
  prefetch: {
    patient: "Patient/{{context.patientId}}",
    encounter: "Encounter?subject={{context.patientId}}&_sort=date",
  },
};
```

The prefetch template includes two keys: `patient`, and `encounter`. `patient` calls for the client to execute a query to fetch the Patients resources. This is a type of FHIR resource \(more on this [here](https://www.hl7.org/fhir/patient.html)\). `Encounter` will return a set of `Encounter` resources sorted by date. This is another kind of FHIR resource \(more on this [here](https://www.hl7.org/fhir/encounter.html)\). 

This will return a FHIR `Patient` and `Bundle` resource respectively. 

### Helper functions

To process the patient's demographic information, such as their name and contact information, make a new file called `util.js` in the same directory as `prefetch-context.js` and copy the following code into it. For the purpose of this walkthrough, we can assume all of this information will be included in the patient FHIR resource \(although this is not guaranteed\).

```javascript
/**
 *
 * @param patient - a fhir patient
 * @returns an array of fhir human names
 * Return an array of patient names from the fhir patient bundle
 */
export function processPatientNames(patient) {
  const patientNames = [];
  patient.name?.forEach((name) => {
    patientNames.push(name);
  });
  return patientNames;
}

/**
 *
 * @param patient - a fhir patient
 * @returns an array of fhir addresses
 * Return an array of addresses from the fhir patient bundle
 */
export function processAddresses(patient) {
  const addresses = [];
  patient.address?.forEach((address) => {
    addresses.push(address);
  });
  return addresses;
}

/**
 *
 * @param patient - a fhir patient
 * @returns an array of fhir contacts
 * Return an array of contacts from the fhir patient bundle
 */
export function processContacts(patient) {
  const contacts = [];
  patient.contact?.forEach((address) => {
    contacts.push(address);
  });
  return contacts;
}

/**
 *
 * @param patient - a fhir patient
 * @returns an array of fhir contact points
 * Return an array of contact points (email and other things) from the fhir patient bundle
 */
export function processTelecom(patient) {
  const telecom = [];
  patient.telecom?.forEach((address) => {
    telecom.push(address);
  });
  return telecom;
}

/**
 *
 * @param encounter
 * @returns an array of FHIR encounter bundles (@todo, no explicit any)
 */
export function processEncounters(encounter) {
  const encounters = [];
  encounter.entry?.forEach((entry) => {
    encounters.push(entry);
  });
  return encounters;
}

/**
 *
 * @param encounter
 * @param daysWithoutAppointment
 * @returns boolean value. If the time difference is beyond the entered threshold,
 * true is returned, o/w false
 */
export function newAppointment(encounter, daysWithoutAppointment) {
  const encounterData = processEncounters(encounter);
  // find most recent and compare it to the current date
  const currentDate = new Date();
  const lastVisit = new Date(encounterData.pop().resource.period.start);
  const timeDifference = currentDate.getTime() - lastVisit.getTime();
  const differenceInDays = Math.floor(timeDifference / (1000 * 3600 * 24));
  if (differenceInDays > daysWithoutAppointment)
    return [true, differenceInDays];
  return [false, differenceInDays];
}

/**
 *
 * @param patient
 * @returns an array of identifiers for the patient
 */
export function getUuid(patient) {
  const identifiers = [];
  patient.identifier?.forEach((entry) => {
    identifiers.push(entry);
  });
  return identifiers;
}

```

Import these functions into `prefetch-context.js`. 

```javascript
import {
  processAddresses,
  processPatientNames,
  processTelecom,
  processEncounters,
  newAppointment,
} from "./util.js";
```

### Service handler

We can access the `patient` resource and the `encounter` resource in the request body. 

```javascript
const handler = async (request) => {
  ...
}
```

The service will return a card corresponding to the pieces of available demographic information. In addition to this, two cards will be returned that convey the total number of encounters on record for patient, and a card conveying if the patient needs to book a new appointment based on the date of the last appointment. This is done in the `lastAppointment()` function. The function returns yes or no depending on the difference between the most recent encounter and the present date in number of days. The function sets the number of days to be 100 by default.

```javascript
const handler = async (request) => {
  const data = request.prefetch;
  const patientNames = processPatientNames(data.patient);
  const addresses = processAddresses(data.patient);
  const telecom = processTelecom(data.patient);
  const encounters = processEncounters(data.encounter);
  const newApp = newAppointment(data.encounter, 100);
  return {
    cards: [
      // Name(s)
      new Card({
        detail: `This patient has ${patientNames.length} name${
          patientNames.length <= 1 ? "" : "s"
        } on record.`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Now seeing: ${patientNames[0].given} ${patientNames[0].family}.`,
        indicator: "info",
      }),
      // DOB
      new Card({
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Date of birth: ${data.patient.birthDate}`,
        indicator: "info",
      }),
      // Active
      new Card({
        detail: `${data.patient.active === true ? "Yes" : "No"}`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Active`,
        indicator: "info",
      }),
      // Address
      new Card({
        detail: `${addresses[0].line}, ${addresses[0].city}, ${addresses[0].state} ${addresses[0].postalCode}`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Current Address`,
        indicator: "info",
      }),
      // Gender
      new Card({
        detail: `${data.patient.gender}`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Gender`,
        indicator: "info",
      }),
      // Telecom (only pulls value of first element in array)
      new Card({
        detail: `${telecom[0].value}`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Contact`,
        indicator: "info",
      }),
      // Information on the last encounter
      new Card({
        detail: `Last visit was on ${
          encounters.pop().resource.period.start
        }. There are ${encounters.length} encounter${
          encounters.length <= 1 ? "" : "s"
        } on record.`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Last visit`,
        indicator: "info",
      }),
      // Seeing the last encounter information
      new Card({
        detail: `Make a new appointment? ${
          newApp[0] === true ? "Yes" : "No"
        }, last appointment was ${newApp[1]} day${
          newApp[1] > 1 ? "s" : ""
        } ago.`,
        source: {
          label: "Automate Medical, Inc.",
          url: "https://www.automatemedical.com/",
        },
        summary: `Book new appointment`,
        indicator: "info",
      }),
    ],
  };
};
```

Export the service.

```javascript
export default new Service(options, handler);
```

### Running the API

In `index.js` , import the service.

{% code title="index.js" %}
```javascript
import { Http, CDSHooks, start } from "@sero.run/sero";

import compareTimeService from "./current-time/current-time.js";
import prefetchContext from "./prefetch-context/prefetch-context.js";

const config = {
  cdsHooks: {
    services: [compareTimeService, prefetchContext],
    cors: true,
  },
};

const http = Http(config);
CDSHooks(config, http);
start(http);
```
{% endcode %}

Run the server with `npm run start`. 

## Deployment

### Logica Sandbox

The [Logica sandbox](https://sandbox.logicahealth.org/) is a service created by [Logica](https://www.logicahealth.org/solutions/fhir-sandbox/) that's useful for developing and testing FHIR applications. For this walkthrough, we are going to take advantage of Logica's ability to act as a CDS client. As opposed to the CDS sandbox, the Logica sandbox provides access to richer patient information, custom data sources and EHRs, richer client flows, and more. 

### Configuring Logica

Head to the Logica sandbox. After creating an account, select the "NEW SANDBOX" button in the "My Sandboxes" section. 

Enter the following information, and select "CREATE."

![Logica sandbox configuration](../../../.gitbook/assets/create_logica_sandbox.png)

Be sure to select FHIR R4, as selecting another version of FHIR will configure Logica differently. The Logica dashboard should now be on-screen.

![Logica sandbox dashboard](../../../.gitbook/assets/logica_dash.png)

Launch ngrok again and enter the command `ngrok http 0.0.0.0:8080` like last time. The public URL will change each time this command is run so be sure to account for that when making requests. 

On the left sidebar, select "CDS Hooks." This is where we'll add the public URL like last time. Select the "+" in the top-right corner. Fill out the form with the following information.

![Registering a CDS Hooks API in the sandbox](../../../.gitbook/assets/logica_register_services.png)

We should now see a screen that looks similar to this one.

![List of registered CDS services in Logica](../../../.gitbook/assets/registered_services_link_1.png)

### Calling the API

When CDS services are registered with Logica, all of the CDS services available at the provided link are listed. The preview shows two services: the service we made in the previous section that fetches the current time, and the service that we made in this section.

Hover over the "Patient view with last encounter" service, and select "Launch." We should be prompted to select a practitioner. Logica simulates a scenario in which this hook would be called - in this case, a doctor named "Susan A. Clark" is the user of the CDS client who will be viewing the profile of a patient in the client's database. After selecting Susan, click on the top patient, Adams, Daniel X, in the list of patients. 

Logica then makes a request to the service and, after some time, responds with a list of cards.

![Response from the service](../../../.gitbook/assets/cds_response_1.png)

Logica, because it is a registered CDS client, sends along the info necessary for us to define prefetch values. If we scroll down some more we should see a card that says the date of the last encounter. 

![Last encounter](../../../.gitbook/assets/last_encounter.png)

Congratulations! We learned how to use context values provided by a CDS client to request additional information from the client to provide more advanced decision support. In the next section, we'll learn how to provide more advanced support through cards, and perform more advanced FHIR queries. 

### Bonus: request and response bodies

Logica lets us view the request and the response bodies whenever a request is made to a service. We can paginate over to them on the cards results page. 

If we take a closer look at the `util.js` file that was provided, we can get a better idea for how to work with FHIR request bundles, and potentially how to handle cases in which data may or may not be present.

