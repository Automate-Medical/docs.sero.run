---
description: Make your first FHIR request
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

FHIR APIs have a base URL that serves as the root against which to make requests.

To test our first FHIR API, we're going to send a request to the FHIR API maintained by [smarthealthit.org](https://www.smarthealthit.org). The base URL for that server is **https://r4.smarthealthit.org.**

The simplest operation we can make is a GET request to /metadata. This endpoint returns a [CapabilityStatement](https://www.hl7.org/fhir/capabilitystatement.html) describing all of the features a particular FHIR API supports. Using `curl` , Postman, or even your browser - try issuing a request to https://r4.smarthealthit.org/metadata.

{% api-method method="get" host="https://r4.smarthealthit.org" path="/metadata" %}
{% api-method-summary %}
Metadata
{% endapi-method-summary %}

{% api-method-description %}
The meta
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="\_format" type="string" required=false %}
One of \`json\` or \`xml\`
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

## 

