---
title: Introduction
keywords: homepage
tags: [getting_started]
sidebar: overview_sidebar
permalink: index.html
toc: true
summary: A brief introduction to getting started.
---

## Scope of this Implementation Guidance

This guidance for the population of a **medicationRequest** resource for the use case of;

**Medication (prescription) requests from a hospital electronic patient medication administration (ePMA) system to a hospital pharmacy system.**

At this time, this guidance is not applicable for the following uses cases;
- Discharge medication requests to the patient's GP
- Primary care medication requests to community pharmacy (aka an FP10)
- Medication requests to a home care medicines provider from a Trust
- Outpatient medication requests dispensed by the hospital pharmacy
- Outpatient medication requests to be dispensed by a community pharmacy (aka an FP10HP)
- Medication requests between two Trusts where there is a local shortage of supply

This guidance is aligned to the following FHIR standards;
- [STU3](https://hl7.org/fhir/STU3/index.html)
- [CareConnect](https://fhir.hl7.org.uk/) based on STU3
- [R4](https://hl7.org/fhir/R4/index.html)

Where guidance relates to a specific version of the FHIR standard, it shall be labelled as such;

[ *STU3* ]

Guidance that only applies to an STU3 implementation...

[ *CareConnect* ]

Guidance that only applies to a CareConnect implementation...

[ *STU3* | *CareConnect* ]

Guidance that applies to either an STU3 or CareConnect implementation...

[ *R4* ]

Guidance that only applies to an R4 implementation...

Where no FHIR standard label is used the guidance is applicable to all three versions of the FHIR standard. 
