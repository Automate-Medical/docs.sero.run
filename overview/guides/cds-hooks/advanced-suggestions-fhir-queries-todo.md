---
description: Links and advanced FHIR queries with Sero
---

# Links, Suggestions, FHIR Queries \(todo\)

## Download starter code \(optional\)

If you’re NOT continuing from the previous lesson, you can download, install, and run the starter code for this lesson below. This sets up a `cds-hooks-api-guide` directory such that it’s identical to the result of the previous lesson.

Again, this is NOT necessary if you’ve just finished the previous lesson.

```bash
git clone (sero-example-repo-url-here)
```

## What you'll be building

In this section, you'll be building a CDS service that calculates the Reynolds Risk score of a patient based on their recent observations, and returns both a useful suggestion based on this information, and a link to a SMART app to further work with the information.

This service will also be invoked with the `patient-view` hook. This hook would be used in a situation where the user of the CDS client was viewing the patients medical record and needed some relevant demographic information.

## Suggestions, links, and advanced FHIR queries

Let's take a closer look at the [attributes](https://cds-hooks.hl7.org/1.0/#card-attributes) of a `Card` from the CDS Hooks specification. There are more attributes of CDS cards that can enhance a services decision support. Two of these attributes are **suggestions** and **links.** 

![](../../../.gitbook/assets/suggestions.png)

![Suggestion and link specification](../../../.gitbook/assets/links.png)

### Suggestions

What if you wanted to provide more interactive decision support, such as suggesting the user read further into an issue, or even prescribe a medication? This is precisely what **suggestions** allow you to do.

Suggestions are described by three attributes, with only a `label`, or a human-readable description of the action, being legible. 

### Links

### Advanced FHIR queries: resources, searching, and sorting

