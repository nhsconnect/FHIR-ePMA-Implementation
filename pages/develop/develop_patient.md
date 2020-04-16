---
title: Patient
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_patient.html
summary: Implementation guidance for populating and consuming the FHIR Patient resource
---

## Introduction

Links to the definitions of the **Patient** resource within the specifications covered within this guidance.
- Patient resource within [STU3](https://www.hl7.org/fhir/STU3/patient.html)
- Patient resource within [CareConnect](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Patient-1)
- Patient resource within [R4](http://hl7.org/fhir/patient.html)

## Minimum Viable Product (MVP)

Elements marked as **MVP** denote those recommended to be required for an MVP for the target use case.

| Elements |  | 
| -- | -- | 
| id | **MVP** | 
| identifier | **MVP** |
| identifier (nhsNumber) | **MVP** |
| active |  |
| name | **MVP** |
| telecom |  |
| gender | **MVP** |
| birthDate | **MVP** |
| deceased |  |
| address |  |
| maritalStatus |  |
| multipleBirth |  |
| photo |  |
| contact |  |
| communication |  |
| generalPractitioner |  |
| managingOrganization |  |
| link |  |
| animal |  |
| other CareConnect extensions |  |

## Patient elements

### id

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Id</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Logical id of this artifact.</td>
  </tr>
</table>

Is is recommended that the logical id is the local patient identifier issued and managed within the Trust for the patient. This will typically be different to the patient's national NHS Number.

### identifier

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Identifier</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Business identifier for this patient.</td>
  </tr>
</table>

For an **STU3** or **R4** implementation record the patient's NHS Number as an identifier.
- The `Patient.identifier.use` should be "official"
- The `Patient.identifier.type` should be "MR"
- The `Patient.identifier.value` must be the patient's NHS Number
- The `Patient.identifier.period` can be omitted unless there is a known validity period for the NHS Number

For a **CareConnect** implementation the **identifier (nhsNumber)** extension should be used for the patient's NHS Number.

Additionally an implementation can populate an additional identifier to record any local patient identifier that is necessary for local business process interoperability.

### identifier (nhsNumber)

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Identifier</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>CareConnect</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>The patient's NHS number.</td>
  </tr>
</table>

Business required for a **CareConnect** implementation as an STU3 extension to record the patient's NHS Number.

### active

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>boolean</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Whether this patient's record is in active use</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

### name

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>HumanName</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A name associated with the patient.</td>
  </tr>
</table>

A single full name, that is the patient's preferred name, must be recorded as a complete string within `name.text`.

The composite name elements of `name.prefix`, `name.given` and `name.family` should be included if available. The complete string used for **name.text** must be the concatenation of these three elements separated by a single whitespace character.

### telecom

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>ContactPoint</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A contact detail for the individual</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

### gender

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>code</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A gender associated with the patient.</td>
  </tr>
</table>

Business required as a key patient demographic for patient identification.

### birthDate

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>date</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Required 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>The date of birth for the individual.</td>
  </tr>
</table>

Business required for two reasons;
- Key patient demographic for patient identification
- Can influence the medication dispensing decision process, e.g. paediatric medication

### deceased[x]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>boolean or dateTime</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Indicates if the individual is deceased or not.</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

### address

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Address</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>An address for the individual.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

The hospital Patient Administration System (PAS) will have a record of the patient address but this information is not required to be shared with the hospital pharmacy system to support the dispensing process.

### maritalStatus 

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>CodeableConcept</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Marital (civil) status of a patient.</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

### multipleBirth[x]

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>boolean or integer</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Whether patient is part of a multiple birth.</td>
  </tr>
</table>   

The element is not required for an MVP implementation.

### photo

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Attachment</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Image of the patient</td>
  </tr>
</table>   

The element is not required for an MVP implementation.

### contact

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>BackboneElement</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A contact party (e.g. guardian, partner, friend) for the patient.</td>
  </tr>
</table>   

The element is not required for an MVP implementation.

### communication

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>BackboneElement</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>A spoken language which may be used to communicate with the patient about his or her health.</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

A local implementation may wish to consider using this element if multi-lingual dispensing instructions are generated within the pharmacy.

### generalPractitioner

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Reference</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Patient's nominated primary care provider.</td>
  </tr>
</table> 

The element is not required for an MVP implementation.

### managingOrganization

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Reference</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Organization that is the custodian of the patient record.</td>
  </tr>
</table>   

The element is not required for an MVP implementation.

### link

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>BackboneElement</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..*</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Link to another patient resource that concerns the same actual person.</td>
  </tr>
</table>  

The element is not required for an MVP implementation.

### animal

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>BackboneElement</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>This patient is known to be an animal (non-human).</td>
  </tr>
</table> 

The element is not required for an MVP implementation.

This element has been removed from the FHIR R4 standard.

### other CareConnect extensions

A number of additional extensions to STU3 were added to the CareConnect standard. All these extensions are not required for an MVP implementation.
- extension (ethnicCategory)
- extension (religiousAffiliation)
- extension (patient-cadavericDonor)
- extension (residentialStatus)
- extension (treatmentCategory)
- extension (nhsCommunication)
- extension (birthPlace)
- extension (nominatedPharmacy)
- extension (deathNotificationStatus)
