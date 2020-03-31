---
title: Develop Overview
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_overview.html
summary: Overarching development principles when using FHIR
---

## Introduction

Some intro blurb...

## Overarching Principles

Stuff to include in this section...

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
