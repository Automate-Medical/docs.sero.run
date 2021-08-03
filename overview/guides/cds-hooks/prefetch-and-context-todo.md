---
description: Processing request data
---

# Prefetch and Context \(todo\)

## Download starter code \(optional\)

If you’re NOT continuing from the previous lesson, you can download, install, and run the starter code for this lesson below. This sets up a `cds-hooks-api-guide` directory such that it’s identical to the result of the previous lesson.

Again, this is NOT necessary if you’ve just finished the previous lesson.

```bash
git clone (sero-example-repo-url-here)
```

## What you'll be building

In this section, you'll be building a CDS service that, when invoked, returns cards displaying demographic information about a patient being viewed by the CDS client. The service will determine if the last encounter date of the patient based on their encounter history, and suggest that an appointment be booked again if it has been too long since their last appointment. 

This service will also be invoked with the `patient-view` hook.

## Prefetch and Context

In the previous example, the service you made didn't require accessing the HTTP `request` body. Although this is not necessary to make a response to a request, services that compute useful recommendations need to access the **contextual** information in the request, and request more **FHIR** data if needed through **prefetch templates**. 

### Context

If you create a CDS Hook \(`patient-view`, `appointment-book`, `encounter-start`, etc.\), for your service to work properly, the CDS client needs to provide important contextual information to your service to work properly. This information is a pre-defined agreement specified by CDS Hooks that guarantees that this information will be provided by the CDS client. 

For example, if you head over to the [specification](https://cds-hooks.org/hooks/patient-view/#context) for the `patient-view` hook \(which we are using in this walkthrough\), you can see that there are a few required keys that need to be provided to the CDS service when a request is made to it by the CDS client. In this example, `userId` and `patientId` are required, and `encounterId` is optional. This is because to perform useful actions for this hook, we need to know the current patient whose record is being viewed, the user who is viewing the record, and we only _might_ need to know the identity of the current encounter. For this example we won't.

In general, it is implied that the CDS client, as a consumer of a service, will send the required values to the service to which it is making a request. As a developer of CDS services, you do not need to worry about providing any additional parameters for context. 

If needed, you could retrieve it from the request body \(you do not need to for this walkthrough\). 

```javascript
const handler = async (request) => {
    const contextData = request.context;
}
```

### Prefetch and prefetch template \(todo\)

What if you need additional information from a FHIR database 

A prefetch is a request that your service makes to the client to execute a FHIR path query. The value for the prefetch template is a FHIR query path.

When we define services, if you need extra data. All you got from the context was the patientId - to do this job, we need some more information. The value can be anything, but the value has to be a FHIR resource path. This is basically a query. You can reference values in the context \(but only values that are castable to a string\). When the client consumes this service, they know it is a patient-view, and that it needs to send some necessary context values. It also sees that there is a prefetch template. If the client is a good client, it will execute the FHIR requests on its FHIR data source, and return the results of the query in an object called prefetch, with a key name matching the key name in the service configuration. 

Configure the values that we want in the pre-fetch template in the `options` variable like last time. The client will then execute the query on their FHIR data source and return it in the request with the name `request.prefetch` 

Remember the context values? This is why the are necessary. 

In general, as a developer of a CDS hook, you should use prefetch templates whenever additional information is needed to perform . They, however, might not be required to perform some tasks. 

### TL;DR

When a CDS client consumes your service, it knows to send important contextual information to the service. This depends on the hook, but expect the client to send these values. 

If your service needs extra information from the client in order to perform a task, you provide a pre-fetch template when configuring your service. When a CDS client goes to make a request to your service, it knows to take the prefetch template, execute the FHIR path queries on its FHIR data source, and return a prefetch object whose keys match the keys of the request. It is common that context fields such as `context.patientId` will be needed to execute these searches - they can be accessed with the double-handlebars syntax, `{{ context.patientId}}`. 

## The code \(todo\)

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

To process this information quickly, you can make a new file called `util.js` and copy the following code into it.

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

You can access the `patient` resource and the `encounter` bundle in the request body. 

```javascript
const handler = async (request) => {
  const data = request.prefetch;
  const patientNames = processPatientNames(data.patient);
  const addresses = processAddresses(data.patient);
  const telecom = processTelecom(data.patient);
  const encounters = processEncounters(data.encounter);
  const newApp = newAppointment(data.encounter, 100);
}
```

Now, make the cards. 

## Deployment \(todo\)

### Logica Sandbox

### Configuring Logica

### Calling our API

Congratulations! You can go to the next section below.



