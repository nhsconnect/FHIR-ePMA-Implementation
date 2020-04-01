---
title: Develop Overview
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_overview.html
summary: Overarching development principles when using FHIR
---

## Introduction

This implementation guidance defines a Minimum Viable Product (MVP) for each FHIR Resource required to support the target use case of medication requests from a hospital ePMA system to a hospital pharmacy system.

An implementation is recommended to adhere to the MVP but can also choose to implement and other elements from the chosen FHIR standard. For the purposes of this guidance, an "implementation" is the partnership between an ePMA system supplier and a pharmacy system supplier within a given Trust.

The MVP uses four FHIR Resources;

![FHIR Resource Relationships (MVP)](images/develop_resources.jpg)

The **MedicationRequest** can reference many other FHIR resources but these four are required for the recommended MVP. 

## Which Version Of The FHIR Standard To Implement?

This guidance aligns with three versions of the FHIR standard; **STU3**, **CareConnect** (UK extension of STU3) and *R4*.

Work is on-going to define a UK-specific version of the R4 standard known as [R4 UK Core](https://simplifier.net/UKCore). Until the implementation of the **MedicationRequest** resource has been published within UK Core, the use of the R4 standard is included here **for information only**, to inform a migration plan from STU3 or CareConnect once the R4 Core UK resources are published as active.

The MVP recommended within the guidance can be implemented with either STU3, CareConnect or R4 so the choice of FHIR standard will be dependent on other factors, such as alignment with existing or parallel integration projects.

Projects at a discovery or early design phase should seek to implement against the R4 Core UK standard unless identified partner systems are already built on STU3 or CareConnect with unsuitable timescales to migrate to R4 Core UK.

## Using FHIR References

The method by which other FHIR resources, e.g. **Medication** or **Patient**, are referenced within the MedicationRequest will be a local implementation decision. There are three options;

 1. Referenced by URL to a FHIR Server
 2. Referenced by an identifier to a resource within the same FHIR Bundle
 3. Referenced by an identifier to a "contained" resource within the MedicationRequest resource

FHIR snippets using XML notation are as follows;

<script src="https://gist.github.com/RobertGoochUK/8cd2ea86de816b00d5cc1e4f3d663194.js"></script>

Using references by URL is the recommended / target solution where FHIR servers are available. These may be future nationally available FHIR servers or locally implemented FHIR servers. When referencing by URL it is recommended that the `reference.display` is populated with appropriate text as per the guidance within this document.

Where a FHIR server is not available or not used within an implementation, the reference by identifier within the same Bundle is the next recommended implementation option.

The use of a contained FHIR resource should be the last option considered. For resources like **Patient** this could introduce duplication within the complete FHIR payload. Also resource **.text** elements should then not be populated. This is because the resource is contained inside the MedicationRequest resource and all text should be represented in the **MedicationRequest.text** element, including data from the contained resource.
