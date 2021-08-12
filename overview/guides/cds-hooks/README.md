---
description: >-
  Create your first clinical decision support API and explore what's possible
  with CDS Hooks
---

# Start a CDS Hooks API

{% hint style="info" %}
Looking for an explanation of CDS Hooks or Decision Support APIs? We cover a broad overview of the topic in [**How to build in health the easy way**](../../../book/how-to-build-in-health/decision-support-apis.md).
{% endhint %}

{% page-ref page="../../../book/how-to-build-in-health/decision-support-apis.md" %}

## Getting started [🏁](https://emojipedia.org/chequered-flag/)

In this walkthrough, we will build three [decision support APIs](../../../book/how-to-build-in-health/decision-support-apis.md) growing in complexity. We will use Sero to implement our APIs according to the CDS Hooks specification.

No prior knowledge of the CDS Hooks specification is necessary but some basic familiarity with FHIR is advised.

The three decision support APIs we will build together are:

1. A service that simply replies with the current time
2. A service that requests patient information and echoes it back
3. A service that processes patient information, calculates a clinical observation, and makes smart suggestions

Let's get started!

## What is "CDS Hooks", anyways? [🤔](https://emojipedia.org/thinking-face/)

> The CDS Hooks specification describes the RESTful APIs and interactions to integrate Clinical Decision Support \(CDS\) between CDS Clients \(typically Electronic Health Record Systems \(EHRs\) or other health information systems\) and CDS Services.

### Services, Clients, and Cards

**CDS Hooks** is a specification describing how to create and use [RESTful APIs](https://en.wikipedia.org/wiki/Representational_state_transfer) to add clinical decision support to health care workflows in existing software like EHRs, patient apps, and backend services.

For example, presenting drug costs transparently to doctors while they are writing prescriptions or assessing the acceptable use of a diagnostic imaging service order are both kinds of things you can build with CDS Hooks.

CDS Services and CDS Clients negotiate the exchange of decision support requests and responses across the RESTful APIs. The framework defines a number of **Hooks** which are pre-agreements about the minimum data requirements for a pre-defined workflow like viewing a patient record or signing a prescription order.

**CDS Clients** are applications that are responsible for making the request to a decision support service.

**CDS Services** are the HTTP APIs that accept requests for decision support made by CDS Clients. Importantly, the specification uses FHIR Resources throughout as a way to exchange clinical data.

Services respond to Client requests with **CDS Cards**. Cards contain decision support information, suggestions, and SMART application links. 



![CDS Hooks workflow](../../../.gitbook/assets/image%20%283%29.png)

To review:

1. A **CDS Client** is an application that makes requests to a decision support service
2. A **CDS Service** is an HTTP API that accepts requests containing patient information and provides decision support responses in the form of CDS Cards
3. A **CDS Card** is a specific recommendation or suggestion made to the user of the CDS Client

We're ready to setup our environment!

