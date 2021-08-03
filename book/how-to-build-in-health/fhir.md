---
description: >-
  Fast Health Interoperability Resources 101 for developers, doctors, founders,
  and patients
---

# FHIR

## What is FHIR [🔥](https://emojipedia.org/fire/)?

{% hint style="success" %}
**FHIR \(Fast healthcare Interoperability Resources\) has many meanings. Here are a few that might help.**
{% endhint %}

✔️ FHIR is a community health information systems standards project and is the [registered trademark of HL7](http://www.hl7.org/index.cfm)

✔️ FHIR is an API \(REST\) standard for health data

✔️ FHIR is a structured document format \(JSON/XML\) for health data

✔️ FHIR is an ONC/CMS ruled transport mechanism for health data

✔️ FHIR is an entry point for patient access, provider directories, formulary APIs, and more

## FHIR is an API + document schema

REST APIs are familiar to developers. FHIR is, in part, a RESTful API over ~150 Resources \(classes, entities, objects, tables, types\). Each Resource has GET, POST, PATCH, etc HTTP operations. Base Resources can be constrained or extended with Profiles that are a kind of a document schema.

{% hint style="success" %}
It's easy to use a FHIR API because it's just REST!
{% endhint %}

{% api-method method="get" host="https://r4.smarthealthit.org/" path="metadata" %}
{% api-method-summary %}
Try your first FHIR request
{% endapi-method-summary %}

{% api-method-description %}
FHIR APIs are required to provide a **CapabilityStatement** at /metadata. You can make a curl request to this public FHIR test server, or even load it in your browser.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
You will receive back a JSON document representation of the CapabilityStatement
{% endapi-method-response-example-description %}

```
{
  "resourceType": "CapabilityStatement",
  "status": "active",
  "date": "2021-08-03T12:54:19-04:00",
  "implementation": {
    "description": "FHIR REST Server",
    "url": "https://r4.smarthealthit.org"
  },
  "fhirVersion": "4.0.0",
  "format": [
    "application/fhir+xml",
    "application/fhir+json"
  ],
  "rest": [ ... ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## FHIR is friendly to patients



## FHIR has momentum and relevance

-

-

-















