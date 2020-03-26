---
title: Development Overview
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_overview.html
summary: Implementation guidance for the FHIR MedicationRequest for the ePMA to Pharmacy use case.
---

This section provides implementation guidance for the use of each element within the **MedicationRequest** FHIR resource, as defined within either the STU3 or R4 standards, or the CareConnect-MedicationRequest-1 standard based on STU3.

Elements listed as MVP "**YES**" are recommended to be supported for a Minimum Viable Product (MVP).

### Resource Elements Common across STU3, CareConnect and R4

The following elements from the MedicationRequest resource are common across STU3, CareConnect and R4.

| Resource Element | MVP | Available Guidance |
| -- | -- | -- |
| [id](develop_medicationrequest_id.html) | YES | Drafted for internal review |
| text | No | Draft in progress |
| identifier | No | _ |
| [status](develop_medicationrequest_status.html) | YES | Drafted for internal review |
| [intent](develop_medicationrequest_intent.html) | YES | Drafted for internal review |
| [category](develop_medicationrequest_category.html) | YES | Drafted for internal review |
| priority | No | _ |
| medicationReference | YES | _ |
| [subject](develop_medicationrequest_subject.html) | YES | Drafted for internal review |
| supportingInformation | No | _ |
| [authoredOn](develop_medicationrequest_authoredon.html) | YES | Drafted for internal review |
| [requester](develop_medicationrequest_requester.html) | YES | Drafted for internal review |
| [recorder](develop_medicationrequest_recorder.html) | No | Drafted for internal review |
| reasonCode | No | _ |
| reasonReference | No | _ |
| [note](develop_medicationrequest_note.html) | No | Drafted for internal review |
| dosageInstruction | YES | _ |
| dispenseRequest | No | _ |
| [substitution](develop_medicationrequest_substitution.html) | YES | Drafted for internal review |
| [priorPrescription](develop_medicationrequest_priorprescription.html) | No | Drafted for internal review |

### Resource Elements Extended with CareConnect-MedicationRequest-1

The following elements have been introduced into the CareConnect standard as extensions.

| Resource Element |  MVP | Available Guidance |
| -- | -- | -- |
| [repeatInformation](develop_medicationrequest_cc_repeatinformation.html) | No | Drafted for internal review |
| [statusReason](develop_medicationrequest_cc_statusreason.html) | No | Drafted for internal review |
| [prescriptionType](develop_medicationrequest_cc_prescriptiontype.html) | No | Drafted for internal review |

### Resource Elements New in FHIR R4

The following elements are only found in FHIR R4.

| Resource Element | MVP | Available Guidance |
| -- | -- | -- |
| statusReason | No | _ |
| doNotPerform | No | _ |
| reported[x] | No | _ |
| encounter | No | _ |
| [performer](develop_medicationrequest_performer.html) | No | Draft in progress |
| [performerType](develop_medicationrequest_performertype.html) | No | Draft in progress |
| instantiatesCanonical | No | _ |
| instantiatesUri | No | _ |
| courseOfTherapyType | No | _ |
| insurance | No | _ |
| dispenseRequest.initialFill | No | _ |
| dispenseRequest.initialFill.quantity | No | _ |
| dispenseRequest.initialFill.duration | No | _ |
| dispenseRequest.dispenseInterval | No | _ |
| dispenseRequest.numberOfRepeatsAllowed | No | _ |

### Resource Elements Removed from FHIR R4 

The following elements have been removed from FHIR R4 but exist within STU3 and CareConnect.

| Resource Element | MVP | Available Guidance |
| -- | -- | -- |
| context | No | _ |
| definition | No | _ |
| [requester.agent](develop_medicationrequest_requester.html) | No | Drafted for internal review |
| [requester.onBehalfOf](develop_medicationrequest_requester.html) | No | Drafted for internal review |

