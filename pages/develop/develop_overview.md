---
title: Development Overview
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_overview.html
summary: Implementation guidance for the FHIR medicationRequest for the ePMA to Pharmacy use case.
---

## Section Title ##

Section contents.

## Element: medicationRequest.intent ##

**Business Meaning**: Describes the nature of the medication request.

[ [STU3](http://hl7.org/fhir/STU3/medicationrequest-definitions.html#MedicationRequest.intent) ]

Mandatory element using the pre-defined and fixed value set of;
**proposal** | **plan** | **order** |  **instance-order**

The value **order** should always be used to denote this is a medication request order.
 
[ [R4](http://hl7.org/fhir/r4/medicationrequest-definitions.html#MedicationRequest.intent) ]

FHIR R4 extends the value set to;
**proposal** | **plan** | **order** | **original-order** | **reflex-order** | **filler-order** | **instance-order** | **option**

The recommendation for the ePMA to Pharmacy use case is to continue to use **order** unless it is locally decided that the extended R4 value set better supports the business requirements.
