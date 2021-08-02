---
description: Building a CDS service with Sero.
---

# Getting Started

To implement a CDS hooks API from scratch, there are a lot of things you need to consider:

* You need to make sure you conform to the CDS hooks minimum specification
* You need to familiarize yourself with CDS hooks and related concepts
* You might want to add custom functionality that could quickly grow in complexity with a custom solution

This is all doable. Yet, with constant updates and questions of conformance, it quickly becomes a chore to build new features using CDS Hooks. 

## Sero makes building in healthcare easy

Sero is a toolkit that makes building a decision support API as easy and fast as possible. Along with this, Sero was made with technologies that ensure you have a great development experience. Sero includes:

* Fastify and AJV server validation
* `Service`, `Card`, and other essential CDS Hooks modules
* Updated specification conformance

## What you'll be building

In this walkthrough, you'll be building a decision support API with support for three CDS hooks. This tutorial serves as an "on-ramp" for building progressively more complicated CDS services. The walkthrough assumes no prior knowledge of CDS hooks or the specification, and some familiarity with FHIR.

The first service you'll build will respond with the current time upon an API call. The second service you'll build will process patient information upon invocation, and display that information. The final service you'll build will process even more patient information, and make smart suggestions based on prior medical observations.

Before building each service, a topic in CDS Hooks or FHIR that will help you accomplish these tasks will be introduced. The scenarios will also be explained in more detail. 

Let's get started!

