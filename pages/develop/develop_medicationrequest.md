---
title: MedicationRequest
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest.html
summary: Implementation guidance for populating and consuming the FHIR MedicationRequest resource
---

# Introduction

Here

# Overarching principles

Here

# MedicationRequest elements

## id

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Id</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Required 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Unique logical identifier for the resource.</td>
  </tr>
</table>

It is highly recommended that the logical id value is a Universally Unique Identifier (UUID) using a standard UUID generator available in most programming languages.

The most comprehensive current definition of the logical id is within the FHIR [R4](https://hl7.org/fhir/R4/resource.html#Resource) standard. The key phrase from the FHIR standard is the logical id is "...*assigned by the server responsible for storing it*".

Vendors have advised that there could be several different scenarios where a MedicationRequest could be stored and it is an implementation decision about where the master MedicationRequest should reside. Possible scenarios for the master MedicationRequest location include;
- ePMA system FHIR Server
- Dispensing system FHIR Server
- Centrally hosted FHIR server (inside hospital network)
- Centrally hosted FHIR server (cloud hosted) **Note**: This would be the scenario when the NHS Electronic Prescription Service implements the FHIR standard.

A further implementation decision is who creates the logical id. The following is in line with the [STU3 FHIR RESTful standards](http://hl7.org/fhir/STU3/http.html#update) and [R4 FHIR RESTful standards](https://hl7.org/fhir/R4/http.html).
-  **Server**:  If the hosting system creates the logical id then the client system would send the MedicationRequest (without an id) as a REST POST command. The created logical id should always be included within the HTTP 201 response so the client can persist this id. For centrally hosted FHIR servers it should always be the hosting system the creates the id so that the server can be responsible for logical id uniqueness.
-  **Client**:  If the client system creates the logical id then the client system would send the MedicationRequest (with an id) as a REST PUT command. The REST PUT command will update a record, but if it does not exist create a new record. If the client system sends the MedicationRequest resource via an asynchronous interoperability pattern then the logical id must be populated with a UUID by the client system. An example would be sending a MedicationRequest within a FHIR payload via the NHS Digital MESH platform.

If either a client or server wants to use an additional business identifier this would be added as an MedicationRequest.identifier and the minimum requirement is:
- A system value: defining the source of the system it has come from
- A value: giving the identifier value

If a client system creates the logical id and there are multiple clients sending MedicationRequests there is a possibility a duplicate logical id occurs. In this event the duplicate id (the second code received) will be rejected with a response stating the logical id is duplicated. The requesting system will need to send the request again with a new logical identifier.

For this reason, within an implementation where multiple clients are POSTing to a FHIR server, it is highly recommenced that the FHIR server creates the logical id to remove the risk of duplication.

<hr/>

## text

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## status

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Code</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Mandatory 1..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A code specifying the current state of the medication order.</td>
  </tr>
</table>

If populated must use a fixed value set defined within the FHIR standard.

It is expected that most implementations will require the use of **status** to support workflow. 

For the purposes of this guidance, the scope of **status** extends to dispensing and administration events. 

| Status | FHIR Definition | Implementation Guidance |
| -- | -- | -- | -- |
| `Draft`  | The prescription is not yet 'actionable', e.g. it is a work in progress, requires sign-off, verification or needs to be run through decision support process. | The order is work in progress within the ePMA system and has not yet sent to the pharmacy. |
| `Active` | The prescription is 'actionable', but not all actions that are implied by it have occurred yet. | The order has been sent and accepted by the pharmacy. Dispensing and administration activities may of started but are not yet complete. |
| `Completed`  | All actions that are implied by the prescription have occurred. | Dispensing and administration activities have been completed for the medication defined within the order. |
| `On Hold` | Actions implied by the prescription are to be temporarily halted, but are expected to continue later. May also be called 'suspended'. | Will prevent the order being sent to the pharmacy. If already sent, an update needs to be sent to the pharmacy to temporarily halt further dispensing. |
| `Cancelled` | The prescription has been withdrawn before any administrations have occurred. | Will prevent the order being sent to the pharmacy. If already sent, an update needs to be sent to the pharmacy so that no further medication is dispensed. |
| `Stopped` | Actions implied by the prescription are to be permanently halted, before all of the administrations occurred. This should not be used if the original order was entered in error. | The order needs to be stopped on clinical grounds. An update needs to be sent to the pharmacy so that no further medication is dispensed. |
| `Entered in Error` | Some of the actions that are implied by the medication request may have occurred. For example, the medication may have been dispensed and the patient may have taken some of the medication. Clinical decision support systems should take this status into account. | The order needs to be stopped due to human data entry error. An update needs to be sent to the pharmacy so that no further medication is dispensed. |
| `Unknown` | The authoring/source system does not know which of the status values currently applies for this observation. Note: This concept is not to be used for 'other' - one of the listed statuses is presumed to apply, but the authoring/source system does not know which. | Recommended not to be supported as the use case for this status value is unclear. |

### Status Transitions 

![Status Transitions](images/medicationrequest_status_diagram.jpg)

| Previous Status | Future Status | Interoperability Guidance |
| -- | -- | -- |
| `Draft` | `Active` | This transition will trigger the sending/sharing of the MedicationRequest from the ePMA system to the pharmacy system to start dispensing activities. Within a RESTful implementation this would be typically implemented as an HTTP POST. |
| `Draft` | `Cancelled` | Contained within the ePMA system. |
| `Draft` | `On-Hold` | Contained within the ePMA system. |
| `On-Hold` | `Draft` | Contained within the ePMA system. |
| `On-Hold` | `Active` | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to restart dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| `Active` | `Active` | Not a MedicationRequest status transition but the pharmacy system would send/share dispensing activities with the ePMA system, typically using a FHIR profile based on **MedicationDispense**. Within a RESTful implementation this would be typically implemented as an HTTP POST. |
| `Active` | `On-Hold` | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to suspend dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| `Active` | `Entered in Error` | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to stop dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| `Active` | `Stopped` | This transition will trigger an update to the MedicationRequest from the ePMA system to the pharmacy system to stop dispensing activities. Within a RESTful implementation this would be typically implemented as either an HTTP PUT or PATCH. |
| `Active` | `Completed` | Contained within the ePMA system. All dispensing activity has been received from the pharmacy system within **MedicationDispense** FHIR resources. The ePMA system has completed the recorded of medicine administration events. |

<hr/>

## statusReason

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>CodeableConcept</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## intent

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>code</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Mandatory 1..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code>  <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Describes the nature of the medication request.</td>
  </tr>
</table>

The value `order` should always be used to denote this is a medication request order.

FHIR R4 extends the value set to; `proposal`, `plan`, `order`, `original-order`, `reflex-order`, `filler-order`, `instance-order` and `option`, but the recommendation for the target use case is to continue to use `order` unless it is locally decided that the extended R4 value set better supports the business requirements.

<hr/>

## category

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>CodeableConcept</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Required 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code>  <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Type of medication usage. Indicates the type of medication request. For example, where the medication is expected to be consumed or administered, i.e. inpatient or outpatient.</td>
  </tr>
</table>

It is expected that any implementation will need to distinguish between medication orders for processes for dispensing and/or administration so this element is business required. 

The STU3 suggested value-set is defined as; `inpatient`, `outpatient` and `community`. The R4 suggested value-set is extended with *discharge*. For a UK implementation, it is recommended to further extend with `leave`.

### Suggested Value-Set

The business meaning for some **Category** values for a UK implementation differs from the FHIR international standard definitions. The suggested value-set applicable for implementation within the UK is as follows;

| Category | Implementation Guidance |
| -- | -- |
| `inpatient` | Requests for medications to be administered on a hospital ward or another acute care setting including Accident and Emergency (A&E). Typically requests would be dispensed by the **hospital pharmacy** and administered to the patient on the ward. |
| `outpatient` | Requests for medication from an outpatient clinic. Typically requests would be dispensed by the **hospital pharmacy** for the patient to self-administer at home. |
| `community` | Requests for medication to be dispensed by a community pharmacy (akin to an NHS FP10HP paper prescription) or other dispenser outside the hospital, such as a Homecare medicines provider. **Note**: This category is likely to be used for all medication requests from Primary Care (e.g. GPs) to community pharmacies or Dispensing Appliance Contractors (akin to an NHS FP10 paper prescription). |
| `discharge` | Requests for medication the patient will take away with them on discharge from an inpatient stay. Typically requests would be dispensed by the **hospital pharmacy** for the patient to self-administer at home. |
| `leave` | Requests for medications that the patient will take away with them during any short break from inpatient care. Typically requests would be dispensed by the **hospital pharmacy** to be self-administered at home with or without the assistance of community based nursing staff. |

For the target ePMA to hospital pharmacy systems use case, it would be expected the the ePMA system is capable to creating medication requests for all five categories. The only category that does not trigger the sending/sharing of a FHIR medicationRequest resource with the hospital pharmacy would be a `community` medication request. A `community` medication request would either trigger the printing and signing of a paper FP10HP prescription, or (when implemented by the Trust) an electronic prescription sent to the NHS Electronic Prescription Service.

<hr/>

## priority

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## medicationReference

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>


## subject

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## supportingInformation

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## authoredOn

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## requester

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## recorder

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## reasonCode

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## reasonReference

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## note

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## dosageInstruction

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## dispenseRequest

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## substitution

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## priorPrescription

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## extension (repeatInformation) [ *CareConnect* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>CareConnect</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## extension (statusReason) [ *CareConnect* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>CareConnect</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## extension (prescriptionType) [ *CareConnect* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>CareConnect</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## statusReason [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## doNotPerform [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## reported[x] [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## encounter [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## performer [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## performerType [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## instantiatesCanonical [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## instantiatesUri [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## courseOfTherapyType [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## insurance [ *R4* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>TBC</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>TBC</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## context [ *STU3* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Reference</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>

## definition [ *STU3* ]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Reference</code></td>
  </tr>
  <tr>
   <td><b>Required/Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>TBC</td>
  </tr>
</table>

<hr/>