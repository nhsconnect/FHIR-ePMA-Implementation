---
title: Introduction
keywords: homepage
tags: [getting_started]
sidebar: overview_sidebar
permalink: index.html
toc: true
summary: A brief introduction to getting started.
---

{% include important.html content="This guidance is DRAFT and under active development by NHS Digital and content may be added or updated on a regular basis." %}

## Scope of this Implementation Guidance

This guidance for the population of a **MedicationRequest** resource for the use case of;

**Medication (prescription) requests from a hospital electronic prescribing and medicines administration (ePMA) system to a hospital pharmacy system for a named patient**

At this time, this guidance is not applicable for the following uses cases;
- Orders for the supply of ward stock medications
- Discharge medication requests to the patient's GP
- Primary care medication requests to community pharmacy (aka an FP10)
- Medication requests to a home care medicines provider from a Trust
- Outpatient medication requests dispensed by the hospital pharmacy
- Outpatient medication requests to be dispensed by a community pharmacy (aka an FP10HCN)
- Medication requests between two Trusts where there is a local shortage of supply

This guidance is aligned to the following FHIR standards;
- [STU3](https://hl7.org/fhir/STU3/index.html)
- [CareConnect](https://fhir.hl7.org.uk/) based on STU3
- [R4](https://hl7.org/fhir/R4/index.html)

This guidance is being incorporated into the on-going work to define a UK-specific implementation of the R4 standard known as [R4 UK Core](https://simplifier.net/UKCore).

## Glossary of Terms

Refer to the [NHS Digital Glossary of Developer Terms](https://digital.nhs.uk/developer/developer-reference/glossary-of-developer-terms).
