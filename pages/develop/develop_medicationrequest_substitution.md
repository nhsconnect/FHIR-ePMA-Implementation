---
title: MedicationRequest.substitution
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_substitution.html
summary: Implementation guidance for MedicationRequest.substitution
---

## Element: MedicationRequest.substitution

**Business Meaning**: Indicates whether or not substitution can or should be part of the dispense. In some cases, substitution must happen, in other cases substitution must not happen. This block explains the prescriber's intent. If nothing is specified substitution may be done.

Within UK healthcare, substitution is not the norm so the international FHIR definition above does not fully apply. It could be unwise to assume all UK implementations will prevent substitution if not explicitly stated, especially if the same clinical system has been previously implemented outside the UK. It is therefore recommended that this element is business required with a default boolean value of "**false**" to denote substitution is **not** allowed.

[ *STU3* / *CareConnect* ]

substitution.allowed = "false"

[ *R4* ]

substitution.allowedBoolean = "false"

### Allowing Substitution

Where substitution to be be allowed, set to "**true**". The inclusion of the coded reason is optional as the value-set defined in FHIR is of limited benefit to UK healthcare.
