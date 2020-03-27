---
title: MedicationRequest.intent
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_intent.html
summary: Implementation guidance for MedicationRequest.intent
---

### intent

**Business Meaning**: Describes the nature of the medication request.

[ *STU3* / *CareConnect* ]

Mandatory element using the pre-defined and fixed value set of; *proposal*, *plan*, *order* and  *instance-order*.

The value **order** should always be used to denote this is a medication request order.
 
[ *R4* ]

FHIR R4 extends the value set to; *proposal*, *plan*, *order*, *original-order*, *reflex-order*, *filler-order*, *instance-order* and *option*.

The recommendation for the ePMA to Pharmacy use case is to continue to use **order** unless it is locally decided that the extended R4 value set better supports the business requirements.

### intent

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Business Required:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
  <tr>
    <td><b>Versions:</b> <code>STU3</code><br/><code>CareConnect</code><br/><code>R4</code></td>
    <td><b>Description:</b> Describes the nature of the medication request.</td>
    <td></td>
  </tr>
</table>

The value `order` should always be used to denote this is a medication request order.

FHIR R4 extends the value set to; `proposal`, `plan`, `order`, `original-order`, `reflex-order`, `filler-order`, `instance-order` and `option`, but the recommendation for the target use case is to continue to use `order` unless it is locally decided that the extended R4 value set better supports the business requirements.
