---
description: Make your first FHIR request. You'll learn about Sero too.
---

# Connect to a FHIR API

{% hint style="info" %}
Looking for an explanation of FHIR? We cover FHIR in [**How to build in health the easy way**](../../book/how-to-build-in-health/fhir.md#what-is-fhir).
{% endhint %}

## What is a FHIR API?

A FHIR API is any HTTP server implementation of the [**FHIR REST API**](https://www.hl7.org/fhir/http.html). Communicating with a FHIR API is an essential task for many developers in health. Sero can be used to make requests to a FHIR API.

FHIR APIs differ in what features and FHIR Resources work with each one. One FHIR API might make available information about insurance plans. Another might make \(authenticated\) access to patient data available.

### Sero supports connecting to FHIR APIs

You can use our FHIR Client to connect to FHIR APIs with JavaScript. See the Sero Reference for a full feature description:

{% page-ref page="../../sero-reference/fhir-client.md" %}

## Try your first FHIR request

{% hint style="danger" %}
You must be able to make HTTP requests to complete this guide - we recommend`curl` or [**Hoppscotch**](https://hoppscotch.io/)\*\*\*\*
{% endhint %}

FHIR APIs have a base URL that serves as the root against which to make requests.

To test our first FHIR API, we're going to send a request to the FHIR API maintained by [smarthealthit.org](https://www.smarthealthit.org). The base URL for that server is **https://r4.smarthealthit.org.**

The simplest operation we can make is a GET request to /metadata. This endpoint returns a [CapabilityStatement](https://www.hl7.org/fhir/capabilitystatement.html) describing all of the features a particular FHIR API supports. Using `curl` , [Postman](https://www.postman.com/), [Hopscotch](https://hoppscotch.io/), or even your browser - try issuing a request to https://r4.smarthealthit.org/metadata.

{% api-method method="get" host="https://r4.smarthealthit.org" path="/metadata" %}
{% api-method-summary %}
Metadata
{% endapi-method-summary %}

{% api-method-description %}
The metadata request returns a Resource describing all of the features of this particular FHIR server. It also contains basic information about the server and API itself. You can use the metadata request to determine if a FHIR API supports a particular FHIR Resource.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="\_format" type="string" required=false %}
One of json or xml
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
This example shows the JSON response, excluding the `rest` key for brevity. 
{% endapi-method-response-example-description %}

```
{
  "resourceType": "CapabilityStatement",
  "status": "active",
  "date": "2021-08-09T15:58:38-04:00",
  "publisher": "Not provided",
  "kind": "instance",
  "implementation": {
    "description": "FHIR REST Server",
    "url": "https://r4.smarthealthit.org"
  },
  "fhirVersion": "4.0.0",
  "format": [
    "application/fhir+xml",
    "application/fhir+json"
  ],
  "rest": [
    ...
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

That's your first FHIR request! 

Another common kind of FHIR API request is _reading_ an individual Resource, like a [DiagnosticReport ](https://www.hl7.org/fhir/diagnosticreport.html)or a [Patient](http://www.hl7.org/fhir/patient.html).

Reading individual Resources is as easy as sending a GET request to `{Resource}/{id}` where {Resource} is the name of the Resource and {id} is the unique identifier for the record you are trying to read.

{% api-method method="get" host="https://r4.smarthealthit.org" path="/Patient/{id}" %}
{% api-method-summary %}
Reading a Resource
{% endapi-method-summary %}

{% api-method-description %}
Reading a Patient, or any Resource, is as simple as knowing the unique ID for the record, and issuing a request where the last part of the path matches the unique ID of the record.  
  
For example, you can try requesting `Patient` with id `87a339d0-8cae-418e-89c7-8651e6aab3c6`.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

You did it! You can learn more about how to connect to FHIR APIs in our [**Client documentation**](../../sero-reference/fhir-client.md) and [**visit HL7.org for more information about the protocol**](http://hl7.org/fhir/).

