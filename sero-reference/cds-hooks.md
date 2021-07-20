# CDS Hooks

Sero can be configured to operate as a decision support API service conforming to the CDS Hooks Service role.

## Conformance

{% hint style="info" %}
We are currently targeting support for [**1.1 STU 2 Ballot \(2020Sep\)**](https://cds-hooks.hl7.org/ballots/2020Sep/) with backwards compatibility for 1.0. 
{% endhint %}

| Capability | Support \(❌/✔️\) | Notes |
| :--- | :---: | :--- |
| GET Discovery Service | ✔️ |  |
| POST Hook Request | ✔️ |  |
| POST Feedback Request | ✔️\* | Minimal support |
| JWT Authorization Support | ❌ |  |
| Hook Request context validation | ✔️ |  |
| Hook Request prefetch validation | ✔️ |  |
| FHIR Authorization workflow | ❌ | Prefetch templates _must_ be filled |
| Creating Services from FHIR PlanDefinitions | ❌ |  |
| TouchStone CDSH 1.0 TestScript Conformance | ✔️\* |  |



