---
title: Practitioner
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_practitioner.html
summary: Implementation guidance for populating and consuming the FHIR Practitioner resource
---

## Introduction

Links to the definitions of the **Practitioner** resource within the specifications covered within this guidance.
- Practitioner resource within [STU3](https://www.hl7.org/fhir/STU3/practitioner.html)
- Practitioner resource within [CareConnect](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Practitioner-1)
- Practitioner resource within [R4](http://hl7.org/fhir/practitioner.html)

## Minimum Viable Product (MVP)

Elements marked as **MVP** denote those recommended to be required for an MVP for the target use case.

| Elements |  | 
| -- | -- | 
| id | **MVP** | 
| text |  | 
| identifier |  | 
| active |  | 
| name | **MVP** | 
| telecom |  | 
| address |  | 
| gender |  | 
| birthDate |  | 
| photo |  | 
| qualification | **MVP** | 
| communication |  | 

## Practitioner elements

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

{% include important.html content="The recommended implementation of the logical id for this resource is under NHS Digital technical review." %}

Until such time as there is an approved and adopted national identifier for NHS staff it is recommended that the logical id is a locally issued employee/user identifier. Such an identifier must be unique across the domain of the Acute Trust and not re-used by another member of staff after someone leaves as this could invalidate historic records.

If no suitable local staff identifier exists then consider using a UUID.

### text

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Narrative</code></td>
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
   <td>Text summary of the resource, for human interpretation.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### identifier

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Identifier</code></td>
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
   <td>An identifier for the person as this agent.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

Where an implementation does not use a locally issued clinician or employee number as the logical [id](develop_practitioner.html#id), such an identifier can be recorded within this element to support local business process interoperability.

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
   <td>Whether this practitioner's record is in active use.</td>
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
   <td>The name(s) associated with the practitioner.</td>
  </tr>
</table>

A single full name, that is the practitioners preferred name, must be recorded as a complete string within `name.text`.

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
   <td>A contact detail for the practitioner (that apply to all roles).</td>
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
   <td>Address(es) of the practitioner that are not role specific (typically home address).</td>
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
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>STU3</code> <code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>The gender of the practitioner.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### birthDate

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>date</code></td>
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
   <td>The date on which the practitioner was born.</td>
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
   <td>Image of the person.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### qualification

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>BackboneElement</code></td>
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
   <td>Certification, licenses, or training pertaining to the provision of care.</td>
  </tr>
</table>

{% include important.html content="The appropriate uri to use when using GMC, NMC or GPhC professional codes has not been confirmed." %}

A business required element to identify the clinical practitioner using their professional code issued by their professional body.
- The `qualifcation.code.coding.system` must be the appropriate uri for the professional body;
  - General Medical Council = https://fhir.hl7.org.uk/Id/gmc-number
  - Nursing and Midwifery Council  = https://fhir.hl7.org.uk/Id/nmc-number
  - General Pharmaceutical Council = https://fhir.hl7.org.uk/Id/gphc-number
- The `qualifcation.code.coding.code` must be the practitioner's professional code issued by their professional body.
- The `qualifcation.code.coding.display` must be the name of the professional body that issued the code, e.g. "*General Medical Council*", "*Nursing and Midwifery Council*" or "*General Pharmaceutical Council*".

### communication 

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>CodeableConceot</code></td>
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
   <td>A spoken language the practitioner can use in patient communication.</td>
  </tr>
</table>

The element is not required for an MVP implementation.
