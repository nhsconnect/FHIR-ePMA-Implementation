---
title: Introduction
keywords: homepage
tags: [getting_started]
sidebar: overview_sidebar
permalink: index.html
toc: true
summary: A brief introduction to getting started.
---

{% include important.html content="This guidance has moved to [ePMA Implementation Guidance for FHIR STU3](https://simplifier.net/guide/epmaimplementationguidanceforfhirstu3)." %}

## Scope of this Implementation Guidance

This guidance for the population of a **MedicationRequest** resource for the use cases of;

- Inpatients
  - Inpatient medication requests, for a named patient, to be dispensed by the hospital pharmacy and intended for administration on a hospital ward
  - Medication requests, for a named patient who is on short-term leave from an inpatient stay (but is not discharged), to be dispensed by the hospital pharmacy and intended for administration at home
  - Discharge medications requests, for a named patient, to be dispensed by the hospital pharmacy and issued on discharge for administration at home
- Outpatients
  - Outpatient medication requests, for a named patient, to be dispensed by the hospital pharmacy and intended for administration in the Outpatients department, Accident and Emergency department, or Day unit
  - Outpatient medication requests, for a named patient, to be dispensed by the hospital pharmacy for administration at home.
  
## Out of Scope for this Version

At this time, this guidance is not applicable for the following uses cases;
- Orders for the supply of ward stock medications
- Primary care medication requests to community pharmacy (aka an FP10)
- Medication requests to a Homecare medicines provider from a Trust
- Outpatient medication requests to be dispensed by a community pharmacy (aka an FP10HNC)
- Medication requests between two Trusts where there is a local shortage of supply.

## Alignment with Standards

This guidance is aligned to the following FHIR standards;
- [STU3](https://hl7.org/fhir/STU3/index.html)
- [CareConnect](https://fhir.hl7.org.uk/) based on STU3
- [R4](https://hl7.org/fhir/R4/index.html)

This guidance is being incorporated into the on-going work to define a UK-specific implementation of the R4 standard known as [R4 UK Core](https://simplifier.net/UKCore).

## Glossary of Terms

Refer to the [NHS Digital Glossary of Developer Terms](https://digital.nhs.uk/developer/developer-reference/glossary-of-developer-terms).
