---
title: Development Overview
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_overview.html
summary: Implementation guidance for the FHIR medicationRequest for the ePMA to Pharmacy use case.
---

This section provides implementation guidance for the use of each element within the **medicationRequest** FHIR resource, as defined within either the STU3 or R4 standards, or the CareConnect-MedicationRequest-1 standard based on STU3.

### Resource Elements Common across STU3, CareConnect and R4

The following elements from the medicationRequest resource are common across STU3, CareConnect and R4.

| Resource Element | Available Guidance |
| -- | -- | -- |
| [id](develop_medicationrequest_id.html) | Drafted for internal review |
| text | Draft in progress |
| identifier | _ |
| [status](develop_medicationrequest_status.html) | Drafted for internal review |
| [intent](develop_medicationrequest_intent.html) | Drafted for internal review |
| [category](develop_medicationrequest_category.html) | Drafted for internal review |
| priority | _ |
| medicationReference | _ |
| subject | _ |
| supportingInformation | _ |
| authoredOn | _ |
| [requester](develop_medicationrequest_requester.html) | Drafted for internal review |
| supportInformation | Draft in progress |
| [recorder](develop_medicationrequest_recorder.html) | Drafted for internal review |
| reasonCode | _ |
| reasonReference | _ |
| [note](develop_medicationrequest_note.html) | Drafted for internal review |
| dosageInstruction | _ |
| dispenseRequest | _ |
| substitution | _ |
| [priorPrescription](develop_medicationrequest_priorprescription.html) | Drafted for internal review |

### Resource Elements Extended with CareConnect-MedicationRequest-1

The following elements have been introduced into the CareConnect standard as extensions.

| Resource Element | Available Guidance |
| -- | -- | -- |
| [repeatInformation](develop_medicationrequest_cc_repeatinformation.html) | Drafted for internal review |
| [statusReason](develop_medicationrequest_cc_statusreason.html) | Drafted for internal review |
| [prescriptionType](develop_medicationrequest_cc_prescriptiontype.html) | Drafted for internal review |

### Resource Elements New in FHIR R4

The following elements are only found in FHIR R4.

| Resource Element | Available Guidance |
| -- | -- | -- |
| statusReason | _ |
| doNotPerform | _ |
| reported[x] | _ |
| encounter | _ |
| performer | Draft in progress |
| performerType | Draft in progress |
| instantiatesCanonical | _ |
| instantiatesUri | _ |
| courseOfTherapyType | _ |
| insurance | _ |
| dispenseRequest.initialFill | _ |
| dispenseRequest.initialFill.quantity | _ |
| dispenseRequest.initialFill.duration | _ |
| dispenseRequest.dispenseInterval | _ |
| dispenseRequest.numberOfRepeatsAllowed | _ |

### Resource Elements Removed from FHIR R4 

The following elements have been removed from FHIR R4 but exist within STU3 and CareConnect.

| Resource Element | Available Guidance |
| -- | -- | -- |
| context | _ |
| definition | _ |
| [requester.agent](develop_medicationrequest_requester.html) | Drafted for internal review |
| [requester.onBehalfOf](develop_medicationrequest_requester.html) | Drafted for internal review |
