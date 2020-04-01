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
| address | **MVP** |
| martialStatus |  |
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



Here

- Patient.identifier.use = "official"
- Patient.identifier.type = "MR"
- Patient.identifier.value = {patient's NHS Number}
- Patient.identifier.period = {any known validity period, omit if unknown}

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

Business required for a CareConnect implementation. An STU3 extension to record the patient's NHS Number.

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
   <td>TBC</td>
  </tr>
</table>  

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
   <td>TBC</td>
  </tr>
</table>  

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
   <td>TBC</td>
  </tr>
</table>  

### address

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Address</code></td>
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
   <td>An address for the individual.</td>
  </tr>
</table>

### martialStatus

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
   <td>TBC</td>
  </tr>
</table>  

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
   <td>TBC</td>
  </tr>
</table>   

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
   <td>TBC</td>
  </tr>
</table>   

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
   <td>TBC</td>
  </tr>
</table>   

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
   <td>TBC</td>
  </tr>
</table>  

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
   <td>TBC</td>
  </tr>
</table> 

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
   <td>TBC</td>
  </tr>
</table>   

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
   <td>TBC</td>
  </tr>
</table>  

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

### other CareConnect extensions

extension (ethnicCategory)
extension (religiousAffiliation)
extension (patient-cadavericDonor)
extension (residentialStatus)
extension (treatmentCategory)
extension (nhsCommunication)
extension (birthPlace)
extension (nominatedPharmacy)
extension (deathNotificationStatus)
