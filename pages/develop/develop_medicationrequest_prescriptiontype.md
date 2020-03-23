---
title: Element: prescriptionType
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_prescriptiontype.html
summary: Implementation guidance for medicationRequest.prescriptionType
---

## Element: medicationRequest.prescriptionType ##

**Business Meaning**: Extension to support the NHS Electronic Prescription Service for the NHSBSA to identify the type of prescription.

[ [STU3] CareConnect Extension ]

It is recommended that this structure is omitted in the Hospital ePMA to Hospital Dispensing system use case.
 
Note the value set for the extension aligns with the legacy HL7v3 'PrescriptionTreatmentType' vocab; **acute** | **repeat** | **repeat dispensing** | **delayed prescribing**. If this extension is also added to FHIR R4 then it should ideally be given a different name.

[ [R4] ]

This extension does not exist within R4.
