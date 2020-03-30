---
title: Patient
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_patient.html
summary: Implementation guidance for populating and consuming the FHIR Patient resource
---

## Introduction

Here

### Overarching principles

For an implementation using CareConnect, replace `patient.identifier` with the extension specific for use with the NHS Number.
 
- Patient.id = a logical id for the resource
- Patient.identifier.use = "official"
- Patient.identifier.type = "MR"
- Patient.identifier.value = {patient's NHS Number}
- Patient.identifier.period = {any known validity period, omit if unknown}
- Patient.name
- Patient.gender
- Patient.birthDate
- Patient.address

[ *CareConnect* ]

CareConnect added a number of extensions to the STU3 Patient resource. The only one relevant to this use case is **identifier (nhsNumber)**. See below for the minimum data set.

[ *STU3* / *R4* ]

Whilst not identical, the elements required to be populated within a **Patient** resource are the same for both versions of FHIR. 

## Patient elements

### id

Here

### identifier

Here

### name

Here

### gender

Here

### birthDate

Here

### address

Here
