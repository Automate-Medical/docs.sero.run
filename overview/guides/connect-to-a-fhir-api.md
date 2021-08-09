---
description: Make your first FHIR request
---

# Connect to a FHIR API

{% hint style="info" %}
Looking for an explanation of FHIR? We cover FHIR in [**How to build in health the easy way**](../../book/how-to-build-in-health/fhir.md#what-is-fhir).
{% endhint %}

## What is a FHIR API?

A FHIR API is any HTTP server implementation of the [**FHIR REST API**](https://www.hl7.org/fhir/http.html). Communicating with a FHIR API is an essential task for many developers in health. Sero can be used to make requests to a FHIR API.

FHIR APIs differ in what features and FHIR Resources work with each one. One FHIR API might make available information about insurance plans. Another might open access.

## Sero supports connecting to FHIR APIs

{% page-ref page="../../sero-reference/fhir-client.md" %}

## Try your first FHIR request

\*\*\*\*[**https://r4.smarthealthit.org/**](https://r4.smarthealthit.org/)\*\*\*\*

You can create your own Sandbox server with Logica Health. Sero's CDS Hooks guides take you through that process as well.

It's just an HTTP API, here are some basic operations to test:

{% api-method method="get" host="https://r4.smarthealthit.org" path="/metadata" %}
{% api-method-summary %}
Metadata
{% endapi-method-summary %}

{% api-method-description %}

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



