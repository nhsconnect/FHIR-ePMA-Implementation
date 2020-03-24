---
title: Element: reasonCode
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_reasoncode.html
summary: Implementation guidance for medicationRequest.reasonCode
---

## Element: medicationRequest.reasonCode ##

**Business Meaning**: Reason or indication for requesting the medication for the patient.

Optional but useful to the wider clinical team as an additional safety check, especially if the requested medication is normally prescribed for different reasons, to avoid confusion between clinical teams. Recording an indication against a medication request also gives valuable insight when data is collated for secondary uses, especially if linked with outcome data.

Where possible this should be a coded term from the SNOMED-CT hierarchy as a descendant of the concept [*insert term*] however but free-text reasons are also acceptable.

[ R4 ]

TBC

FHIR says descendants of 404684003 (Clinical finding).

FHIR 4 has several additional structures here.
