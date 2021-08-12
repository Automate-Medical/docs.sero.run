---
description: 'A short 101 guide for developers, doctors, founders, and patients'
---

# FHIR

## What is FHIR [🔥](https://emojipedia.org/fire/)?

{% hint style="success" %}
**FHIR is an acronym \(Fast Healthcare Interoperability Resources\) and is pronounced like "fire"**
{% endhint %}

**FHIR is an interface for structured health data.** FHIR is also:

✔️ A [**community health information systems standards project**](https://www.hl7.org/fhir/) and is the [registered trademark of HL7](http://www.hl7.org/index.cfm)

✔️ An [**API \(REST\)**](https://www.hl7.org/fhir/http.html) standard and structured document format \(JSON/XML\) for health data

✔️ An [**ONC/CMS ruled transport mechanism for health data**](https://www.healthit.gov/topic/standards-technology/standards/fhir-fact-sheets)\*\*\*\*

✔️ A new way for [**developers, doctors, and patients to build applications**](https://www.automatemedical.com/) that use and transform health data

## API + document schema

REST APIs are familiar to developers. FHIR is, in part, a RESTful API over ~150 Resources \(classes, entities, objects, tables, types\). Each Resource has GET, POST, PATCH, etc HTTP operations. Base Resources can be constrained or extended with Profiles that are a kind of a document schema. Documents are formatted as JSON and XML.

{% hint style="success" %}
**FHIR is easy to use for developers because it exposes conventional API patterns from other industries to health care data specifically**
{% endhint %}

A FHIR Resource formatted as JSON looks something like this:

{% tabs %}
{% tab title="JavaScript" %}
```javascript
{
  "resourceType": "Patient",
  "id": "newborn",
  "gender": "male",
  "birthDate": "2021-08-05",
}
```
{% endtab %}
{% endtabs %}

JSON is the world's most popular structured data storage format, and so it's compatible with every development environment. [Sero](https://docs.sero.run/)'s quickstart guide has some practical starting points for developers:

## Patient friendly

FHIR powers patient access to health data like current and past medications, immunization history, allergies, diagnostic reports, clinical notes, care plans and more. 

Patient-directed access to FHIR data sources is a significant initiative in the United States and operates under the umbrella term "SMART":

> SMART Health IT was launched with [a New England Journal of Medicine article](https://www.nejm.org/doi/full/10.1056/NEJMp0900411) proposing a universal API \(application programming interface\) to transform EHRs into platforms for substitutable iPhone-like apps

With FHIR + SMART, patient-directed access to health data is not only possible - but available in totally transparent and open ways.

{% page-ref page="smart-apps.md" %}

## Relevance

FHIR is actively used, required for use, or suggested for use in a number of public and private sector projects, but most interestingly in:

* [Apple Health is built on FHIR](https://www.apple.com/healthcare/health-records/)
* [Argonaut Project is a unified private sector project from Apple, Microsoft, Epic, Cerner, Intermountain Healthcare and others to build next generation health systems on FHIR](https://argonautwiki.hl7.org/w/images/argonautwiki.hl7.org/1/17/Argonaut_Project_Background_and_Overview_Presentation.pdf)
* [21st Century Cures Act](https://www.healthit.gov/curesrule/)
* [Interoperability and Patient Access final rule \(CMS-9115-F\) explicitly requires FHIR APIs](https://www.cms.gov/Regulations-and-Guidance/Guidance/Interoperability/index#CMS-Interoperability-and-Patient-Access-Final-Rule) 
* [SMART Health IT makes patient directed access possible](https://smarthealthit.org/)
* [Health Cards, the emerging global immunization record standard, are built on FHIR](https://smarthealth.cards/)

## Is FHIR the only standard?

**No!** FHIR is generally complementary to other standards though. In addition to FHIR, you might hear about:

* HL7 V2
* DICOM
* OMOP

\*\*\*\*











