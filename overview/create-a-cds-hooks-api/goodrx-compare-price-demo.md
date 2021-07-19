# GoodRx CDS Price Comparison

## Overview

GoodRx.

## Code walkthrough

We start by important Sero's HTTP and CDS Hooks modules. The GoodRx Price Demo shows us how 

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import { Http, CDSHooks } from "@sero.run/sero"
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="TypeScript" %}
```typescript
const options = {
  id: "good-rx-comparison"
  title: "GoodRx Compare Price Service for MedicationRequest"
  hook: "order-select"
  description: "GoodRx's Compare Price API is used to provide a drug cost estimate",
};
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="TypeScript" %}
```typescript
const handler = async (request) => {
  const { draftOrders }: { draftOrders: Bundle } = request.context;
  
  const medicationRequest = draftOrders.entry
    ?.find((e) => e.resource?.resourceType == "MedicationRequest")
    ?.resource as MedicationRequest

  if (!medicationRequest) throw new NoDecisionResponse();

  const response = await comparePrice({ name:  });
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="TypeScript" %}
```typescript
const goodRxService = new CDSHooks.orderSelectService(options, handler)
```
{% endtab %}
{% endtabs %}

## 

## Running it locally

### Clone the example

Becoming a super hero is a fairly straight forward process:

```bash
$ git clone https://github.com/automate-medical/goodrx-price-demo
$ cd good-rx-price-demo
```

### Install and start

{% hint style="info" %}
You'll need to have Node &gt;= 14 installed on your platform. 
{% endhint %}

From inside of the freshly cloned repository run:

```bash
npm install
```

Next you need to congfiu

### Running in the CDS Hooks Sandbox





