---
description: Getting started with CDS hooks
---

# What Is CDS Hooks?

### What is CDS Hooks?

CDS hooks is a specification describing how to create RESTful APIs and interactions to integrate CDS between CDS clients and CDS services. 

To work with Sero, you only need to be familiar with a few core things. 

### What is CDS?

**CDS** stands for "clinical decision support." Clinical decision support is a framework for providing clinical information to healthcare workers in a timely manner. Usually this takes the form of providing healthcare workers information about a patient at the point of care to improve decisions, thus improving patient outcomes.

CDS can be as simple as providing an administrative assistant the name of the patient's general practitioner. Or, it can be as complicated as recommending a prescription a patient should be prescribed given past clinical observations. That same service could also contact an external API to provide the doctor with the cheapest prescription option available. 

### CDS Clients, services, and cards

A **CDS client** is anything that can consume CDS. In the context of CDS hooks, this means consume responses from CDS services.

A **CDS service** is an API that accepts requests containing patient information and provides responses in the form of CDS cards. 

A **CDS card** is a specific recommendation or suggestion made to the user of the CDS client. Going by the previous example of the administrative assistant, a service that responds with this information could return a JSON object card with the general practitioners name, and telephone number, as two discrete cards. Each card is a JSON object. Information returned in cards is usually displayed to the user within a UI element. It is called a card as it is common for the UI element to look like a card. 

### Current specification

The CDS hooks specification goes deeper in a number of areas - only some of which is going to be covered in this walkthrough. If you are curious and want to read more about the specification, it can be found here. 

