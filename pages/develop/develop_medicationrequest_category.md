---
title: medicationRequest.category
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_category.html
summary: Implementation guidance for medicationRequest.category
---

## Element: medicationRequest.category

**Business Meaning**: Type of medication usage. Indicates the type of medication request. For example, where the medication is expected to be consumed or administered, i.e. inpatient or outpatient.

An optional element which a suggested value-set. It is expected that any implementation will need to distinguish between medication orders for processes for dispensing and/or administration. 

[ *STU3* / *CareConnect* ]

The STU3 suggested value-set is defined as; *inpatient*, *outpatient* and *community*. 

[ *R4* ]

The R4 suggested value-set is defined as; *inpatient*, *outpatient*, *community* and *discharge*. 

### Suggested Value-Set and Implementation Guidance

The suggested value-set applicable for implementation within the UK is as follows;

| Category | Implementation Guidance |
| -- | -- |
| **inpatient** | Requests for medications to be administered on a hospital ward or another acute care setting including Accident and Emergency (A&E). Typically requests would be dispensed by the **hospital pharmacy** and administered to the patient on the ward. |
| **outpatient** | Requests for medication from an outpatient clinic. Typically requests would be dispensed by the **hospital pharmacy** for the patient to self-administer at home. |
| **community** | Requests for medication to be dispensed by a community pharmacy (akin to an NHS FP10HP paper prescription) or other dispenser outside the hospital, such as a Homecare medicines provider. **Note**: This category is likely to be used for all medication requests from Primary Care (e.g. GPs) to community pharmacies or Dispensing Appliance Contractors (akin to an NHS FP10 paper prescription). |
| **discharge** | Requests for medication the patient will take away with them on discharge from an inpatient stay. Typically requests would be dispensed by the **hospital pharmacy** for the patient to self-administer at home. |
| **leave** | Requests for medications that the patient will take away with them during any short break from inpatient care. Typically requests would be dispensed by the **hospital pharmacy** to be self-administered at home with or without the assistance of community based nursing staff. |

For the target ePMA to hospital pharmacy systems use case, it would be expected the the ePMA system is capable to creating medication requests for all five categories. The only category that does not trigger the sending/sharing of a FHIR medicationRequest resource with the hospital pharmacy would be a **community** medication request. A **community** medication request would either trigger the printing and signing of a paper FP10HP prescription, or (when implemented by the Trust) an electronic prescription sent to the NHS Electronic Prescription Service.
