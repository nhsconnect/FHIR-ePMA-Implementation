---
title: medicationRequest.requester
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_requester.html
summary: Implementation guidance for medicationRequest.requester
---

## Element: medicationRequest.requester

**Business Meaning**: The clinician requesting the medication.

Recommended as a mandatory element for most implementations.

Recommended to be the prescribing clinician recorded on the ePMA system for the medication request, as a reference to a FHIR **Practitioner** resource.

The requester can be a reference to a number of different FHIR resources; *Practitioner*, *PractitionerRole*, *Organization*, *Patient*, *RelatedPerson* or *Device*. For this use case it is recommended to always use **Practitioner** unless an implementation supports use cases like requests direct from patients or automated requests from medical or monitoring devices.

### Additional Guidance

Where an implementation does not currently record the prescribing clinician then consider the following;
- If the prescribing clinician is authorising new medication then populate with their details.
- If the prescribing clinician is re-ordering from a previous medication request that they authorised then populate with their details, and consider populating [priorPrescription](develop_medicationrequest_priorPrescription.html).
- If the prescribing clinician is acting on behalf of a colleague to authorise new medication then populate with the details of the colleague and consider also populating [recorder](develop_medicationrequest_recorder.html).
- If the prescribing clinician is re-ordering from a previous medication request authorised by a colleague then populate with their details (not the colleagues) and consider populating [priorPrescription](develop_medicationrequest_priorPrescription.html).
- If the prescribing clinician is acting on behalf of a colleague to re-order from a previous medication request authorised by someone else then populate with the details of the colleague and consider also populating [recorder](develop_medicationrequest_recorder.html) and [priorPrescription](develop_medicationrequest_priorPrescription.html).

**Note**: If the user is not a qualified prescriber but performing the task of data entry then they are instead acting as the [recorder](develop_medicationrequest_recorder.html).

**TBC**: What if a nurse is requesting more supply of a drug from an original prescription?
