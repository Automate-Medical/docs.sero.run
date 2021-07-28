---
description: Get information to doctors in the places they're already working
---

# Decision Support APIs

## What is a decision support API?

{% hint style="success" %}
\*\*\*\*[**Decision Support APIs are a supported feature in Sero.**](../../overview/user-guides/start-a-cds-hooks-api/)\*\*\*\*
{% endhint %}

A decision support API supports an existing health care workflow such as prescribing medication, by providing contextually relevant information, automation, and guidelines related to that workflow via a standardized API. 

With decision support APIs we can build examples like:

* [Automating the identification of high risk medication order requests](http://build.fhir.org/ig/cqframework/opioid-cds/) via the CDC Guideline for Prescribing Opioids for Chronic Pain
* Enforcing [Acceptable Use Criteria for diagnostic imaging service requests](https://www.cms.gov/Medicare/Quality-Initiatives-Patient-Assessment-Instruments/Appropriate-Use-Criteria-Program) like CTs, PETs, and MRIs
* Presenting drug costs transparently to doctors when they are writing prescriptions

According to Dr. Joe Kimura, Chief Medical Officer at Atrius Health:

> The amount of information we need to understand is getting so untenable that it’s unreasonable to expect the average clinician to integrate all of it into their decision-making effectively and reliably

Decision Support APIs help to create health care workflows that reduce burn out for doctors and raise the quality of care for patients.

## How do decision support APIs work?

[Decision Support APIs have a long history](https://joshuakelly.substack.com/p/40-years-of-healthcare-decision-support). The current open standard is called [CDS Hooks](https://cds-hooks.hl7.org/).

### CDS Hooks

> The CDS Hooks specification describes the RESTful APIs and interactions to integrate Clinical Decision Support \(CDS\) between CDS Clients \(typically Electronic Health Record Systems \(EHRs\) or other health information systems\) and CDS Services.

A decision support API built with CDS Hooks is a RESTful HTTP API. 

![](../../.gitbook/assets/image.png)

### Discovery

### Requesting

## Relevant 

