---
description: Get information to doctors in the places they're already working
---

# Decision Support APIs

## What is a decision support API?

{% hint style="success" %}
\*\*\*\*[**Decision Support APIs are a supported feature in Sero.**](../../overview/guides/cds-hooks/)\*\*\*\*
{% endhint %}

A decision support API supports an existing health care workflow such as prescribing medication, by providing contextually relevant information, automation, and guidelines related to that workflow via a standardized API. 

With decision support APIs we can build examples like:

* \*\*\*\*[**Automating the identification of high risk medication order requests**](http://build.fhir.org/ig/cqframework/opioid-cds/) via the CDC Guideline for Prescribing Opioids for Chronic Pain
* Enforcing ****[**Acceptable Use Criteria for diagnostic imaging service requests**](https://www.cms.gov/Medicare/Quality-Initiatives-Patient-Assessment-Instruments/Appropriate-Use-Criteria-Program) like CTs, PETs, and MRIs
* Presenting drug costs transparently to doctors when they are writing prescriptions

According to Dr. Joe Kimura, Chief Medical Officer at Atrius Health:

> The amount of information we need to understand is getting so untenable that it’s unreasonable to expect the average clinician to integrate all of it into their decision-making effectively and reliably

Decision Support APIs help to create health care workflows that reduce burn out for doctors and raise the quality of care for patients.

## How do decision support APIs work?

[Decision Support APIs have a long history](https://joshuakelly.substack.com/p/40-years-of-healthcare-decision-support). The current open standard is called [**CDS Hooks**](https://cds-hooks.hl7.org/). The

### CDS Hooks

> The CDS Hooks specification describes the RESTful APIs and interactions to integrate Clinical Decision Support \(CDS\) between CDS Clients \(typically Electronic Health Record Systems \(EHRs\) or other health information systems\) and CDS Services.

A decision support API built with CDS Hooks is a RESTful HTTP API. CDS Services and CDS Clients negotiate the exchange of decision support requests and responses. The framework defines a number of `hooks` which are pre-agreements about the minimum data requirements for a pre-defined workflow like viewing a patient record or signing a prescription order.

![The CDS Hooks workflow](../../.gitbook/assets/image.png)

CDS Services advertise their capabilities through a Discovery endpoint. Clients \(like an EHR\) trigger these capabilities. Clients provide FHIR Resources as required by the `hook` in the form of `context` and `prefetch` parameters. Services execute their own rules and return one or many Cards that present information, provide actionable suggestions, and initiate SMART App launch sequences.

Learn more about how to launch a CDS Hooks API in our Sero user guide. 

{% page-ref page="../../overview/guides/cds-hooks/" %}

## Relevance

CDS Hooks are actively used, required for use, or suggested for use in a number of places in addition to private sector projects.

* [Da Vinci Coverage Requirements Discovery \(CRD\) Implementation Guide](http://hl7.org/fhir/us/davinci-crd/)
* [Da Vinci Documentation Templates and Rules \(DTR\) Implementation Guide](http://hl7.org/fhir/us/davinci-dtr/history.html)
* [PAMA Accessible Use Criteria](https://argonautproject.github.io/cds-hooks-for-pama/)
* [ARHQ CDS Connect](https://cds.ahrq.gov/cdsconnect)
* [CDC Opioid Prescribing Support Implementation Guide](http://build.fhir.org/ig/cqframework/opioid-cds/)
* [Epic CDS Hook Support](https://open.epic.com/Content/specs/staged/Epic%20CDS%20Hooks%20Support.pdf)

