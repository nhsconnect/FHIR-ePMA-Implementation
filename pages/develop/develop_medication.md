---
title: Medication
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medication.html
summary: Implementation guidance for populating and consuming the FHIR Medication resource
---

## Introduction

Links to the definitions of the **Medication** resource within the specifications covered within this guidance.
- Medication resource within [STU3](https://www.hl7.org/fhir/STU3/medication.html)
- Medication resource within [CareConnect](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Medication-1)
- Medication resource within [R4](http://hl7.org/fhir/medication.html)

## Minimum Viable Product (MVP)

Elements marked as **MVP** denote those recommended to be required for an MVP for the target use case.

| Elements |  | 
| -- | -- | 
| id | **MVP** | 
| text |  | 
| identifier |  | 
| code | **MVP** | 
| status |  | 
| manufacturer |  | 
| form |  | 
| amount |  | 
| ingredient |  | 
| batch |  | 
| isBrand |  | 
| isOverTheCounter |  | 
| package |  | 
| image |  | 

## Medication elements

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

It is recommended this is the medication **unique dm+d concept id**. This use of this identifier will provide a unique mechanism to return a Medication resource in a RESTful implementation anywhere across the NHS.

For example;

`<reference value="https://myFHIRserver/medication/87652004"/>`

Where `87652004` in this example is the unique dm+d concept id for the Virtual Therapeutic Moiety for **Atenolol**.

**Note**: Where a medication is not within the dm+d and therefore does not have a dm+d code then do not use a Medication resource. See [medication with no dm+d code](develop_medicationrequest.html#requested-medication-with-no-dmd-code).

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
   <td>Text summary of the resource, for human interpretation</td>
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
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Business identifier for this medication.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### code

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>CodeableConcept</code></td>
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
   <td>A code (or set of codes) that specify this medication, or a textual description if no code is available. Usage note: This could be a standard medication code such as a code from RxNorm, SNOMED CT, IDMP etc. It could also be a national or local formulary code, optionally with translations to other code systems.</td>
  </tr>
</table>

All medication must be represented using NHS dm+d terminology.
- The `code.coding.system` must be "http://snomed.info/sct".
- The `code.coding.code` must be the NHS dm+d concept code.
- The `code.coding.display` must be the NHS dm+d concept description.		

**Note**: The dm+d standard may change the identifier for a medication concept and will publish the current and previous identifier together with the date of the change. A dm+d FHIR terminology server therefore may return two codes for a given medication. For example;

<script src="https://gist.github.com/RobertGoochUK/f1c91565d53e94b53a1d27f23c8db5eb.js"></script>

### status

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
   <td>A code to indicate if the medication is in active use.</td>
  </tr>
</table>

{% include important.html content="The use of the 'status' element within the recommended MVP is under NHS Digital review." %}

Guidance to follow...

### manufacturer

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
   <td>Describes the details of the manufacturer of the medication product. This is not intended to represent the distributor of a medication product.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

Within the dm+d terminology, the AMP and AMPP concepts include a coded manufacturer.

### form

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
   <td>Describes the form of the item, e.g. powder, tablets, capsule etc.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

Within the dm+d terminology, the VMP, AMP, VMPP and AMPP concepts include a coded form.

### amount

<table class='resource-attributes'>
  <tr>
   <td><b>Data Type:</b></td>
   <td><code>Ratio</code></td>
  </tr>
  <tr>
   <td><b>Required / Cardinality:</b></td>
   <td>Optional 0..1</td>
  </tr>
  <tr>
    <td><b>Version Support:</b> </td>
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Specific amount of the drug in the packaged product. For example, when specifying a product that has the same strength (For example, Insulin glargine 100 unit per mL solution for injection), this attribute provides additional clarification of the package amount (For example, 3 mL, 10mL, etc.).</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### ingredient

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
   <td>Identifies a particular constituent of interest in the product.</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### batch

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
    <td><code>R4</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Information that only applies to packages (not products).</td>
  </tr>
</table>

The element is not required for an MVP implementation.

### isBrand

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
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Set to true if the item is attributable to a specific manufacturer.</td>
  </tr>
</table>

This element has been removed from FHIR R4 so should not be implemented as part of an STU3 or CareConnect implementation. 

Within the dm+d terminology, medication that is a brand is identified as an AMP and AMPP concept.

### isOverTheCounter

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
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Set to true if the medication can be obtained without an order from a prescriber.</td>
  </tr>
</table>

This element has been removed from FHIR R4 so should not be implemented as part of an STU3 or CareConnect implementation. 

### package

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
   <td>Information that only applies to packages (not products).</td>
  </tr>
</table>

This element has been removed from FHIR R4 so should not be implemented as part of an STU3 or CareConnect implementation. 

### image

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
    <td><code>STU3</code></td>
  </tr>
  <tr>
   <td><b>Description:</b></td>
   <td>Photo(s) or graphic representation(s) of the medication.</td>
  </tr>
</table>

This element has been removed from FHIR R4 so should not be implemented as part of an STU3 or CareConnect implementation. 
