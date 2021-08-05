---
description: 'Access information about Insurance Plans, Coverage, Network'
---

# Provider Directory

## What is a provider directory?

{% hint style="success" %}
**Provider directory access is a supported feature in Sero, contact fou**[**nders@automatemedical.com** ](mailto:founders@automatemedical.com)\*\*\*\*
{% endhint %}

Provider directories are databases containing formation about insurance plans, practitioners \(like doctors and specialists\) and their roles \(the specific services offered\).

> Provider directories play a critical role in enabling identification of individual providers and provider organizations, as well as characteristics about them. Provider directories support a variety of use cases. 
>
> \*\*\*\*[**DaVinci PDEX Plan Net**](https://build.fhir.org/ig/HL7/davinci-pdex-plan-net/)\*\*\*\*

Provider directories help to answer questions about:

* Finding specialist service providers for specific medical services
* Which providers, primary care doctors, specialists, pharmacies, facilities are "in network" for a given plan
* Accessibility and scheduling information, office hours, spoken languages
* Organizations that provide health care services, available insurance plans, coverage locations

## How do provider directories work?

In the United States, CMS regulated health plans are required to publish a public-facing [**FHIR API**](fhir/). Major plan payers like Humana, Aetna, and Optum have implemented a specific API called [**Da Vinci PDex Plan Net**](http://hl7.org/fhir/us/davinci-pdex-plan-net/STU1/). 

Provider directories typically implement these FHIR Resources:

* [InsurancePlan](http://hl7.org/fhir/R4/insuranceplan.html)
* [Practitioner](http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-practitioner.html)
* [PractitionerRole](http://hl7.org/fhir/R4/practitionerrole.html)
* [HealthcareService](http://hl7.org/fhir/R4/healthcareservice.html)
* [Organization](http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-organization.html)
* [Location](http://hl7.org/fhir/us/core/STU3.1/StructureDefinition-us-core-location.html)

These are made available for third party application developers to query against. You can use the Sero Client library to easily make paginated search queries to these provider directories. 

A simple illustration of the architecture:

![An example Plan Net architecture implementation of a Provider Directory ](../../.gitbook/assets/image%20%281%29.png)

Try out this example with a real Provider Directory API and the Sero toolkit:

{% page-ref page="../../overview/examples/humana-hematology-specialist-search.md" %}



