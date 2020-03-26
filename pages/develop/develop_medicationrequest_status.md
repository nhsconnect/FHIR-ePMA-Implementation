---
title: MedicationRequest.status
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_status.html
summary: Implementation guidance for MedicationRequest.status
---

## Element: MedicationRequest.status

**Business Meaning**: A code specifying the current state of the medication order.

If populated must use a fixed value set defined within the FHIR standard.

It is expected that most implementations will require the use of **status** to support workflow. 

For the purposes of this guidance, the scope of **status** extends to dispensing and administration events. 

| Status | FHIR Definition | Implementation Guidance |
| -- | -- | -- | -- |
| Draft  | The prescription is not yet 'actionable', e.g. it is a work in progress, requires sign-off, verification or needs to be run through decision support process. | The order is work in progress within the ePMA system and has not yet sent to the pharmacy. |
| Active | The prescription is 'actionable', but not all actions that are implied by it have occurred yet. | The order has been sent and accepted by the pharmacy. Dispensing and administration activities may of started but are not yet complete. |
| Completed  | All actions that are implied by the prescription have occurred. | Dispensing and administration activities have been completed for the medication defined within the order. |
| On Hold | Actions implied by the prescription are to be temporarily halted, but are expected to continue later. May also be called 'suspended'. | Will prevent the order being sent to the pharmacy. If already sent, an update needs to be sent to the pharmacy to temporarily halt further dispensing. |
| Cancelled | The prescription has been withdrawn before any administrations have occurred. | Will prevent the order being sent to the pharmacy. If already sent, an update needs to be sent to the pharmacy so that no further medication is dispensed. |
| Stopped | Actions implied by the prescription are to be permanently halted, before all of the administrations occurred. This should not be used if the original order was entered in error. | The order needs to be stopped on clinical grounds. An update needs to be sent to the pharmacy so that no further medication is dispensed. |
| Entered in Error | Some of the actions that are implied by the medication request may have occurred. For example, the medication may have been dispensed and the patient may have taken some of the medication. Clinical decision support systems should take this status into account. | The order needs to be stopped due to human data entry error. An update needs to be sent to the pharmacy so that no further medication is dispensed. |
| Unknown | The authoring/source system does not know which of the status values currently applies for this observation. Note: This concept is not to be used for 'other' - one of the listed statuses is presumed to apply, but the authoring/source system does not know which. | Recommended not to be supported as the use case for this status value is unclear. |

### ePMA/Pharmacy Interoperability for Status Transitions

![Status Transitions](images/medicationrequest_status_diagram.jpg)

| Previous Status | Future Status | Interoperability Guidance |
| -- | -- | -- |
| Draft | Active | This transition will trigger the sending/sharing of the MedicationRequest from the ePMA system to the pharmacy system to start dispensing activities. Within a RESTful implementation this would be typically implemented as an HTTP POST. |
| Draft | Cancelled | Contained within the ePMA system. |
| Draft | On-Hold | Contained within the ePMA system. |
| On-Hold | Draft | Contained within the ePMA system. |
| On-Hold | Active | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to restart dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| Active | Active | Not a MedicationRequest status transition but the pharmacy system would send/share dispensing activities with the ePMA system, typically using a FHIR profile based on **MedicationDispense**. Within a RESTful implementation this would be typically implemented as an HTTP POST. |
| Active | On-Hold | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to suspend dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| Active | Entered in Error | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to stop dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| Active | Stopped | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to stop dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| Active | Completed | Contained within the ePMA system. All dispensing activity has been received from the pharmacy system within **MedicationDispense** FHIR resources. The ePMA system has completed the recorded of medicine administration events. |
