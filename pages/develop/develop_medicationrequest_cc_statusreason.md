---
title: medicationRequest.statusReason
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_cc_statusreason.html
summary: Implementation guidance for medicationRequest.statusReason
---

## Element: medicationRequest.statusReason

**Business Meaning**: Extension to support the workflow status values used by the NHS Electronic Prescription Service.

[ STU3 ]

This element does not exist within STU3.

[ CareConnect ]

It is recommended that this structure is omitted in the Hospital ePMA to Hospital Dispensing system use case.

[ R4 ]

FHIR R4 introduces a 'statusReason' into the international standard but this serves a completely different purpose to the UK extension 'statusReason' within the STU3 version of FHIR. The R4 'statusReason' is to record a coded reason why medication was stopped, cancelled, etc. opposed to the status within the workflow of prescribing and dispensing. The use of 'status' and 'statusReason' for a primary care (EPS) implementation will need working through with potentially an extension to support the business needs for the EPS.