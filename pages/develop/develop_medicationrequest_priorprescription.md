---
title: medicationRequest.priorPrescription
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_priorprescription.html
summary: Implementation guidance for medicationRequest.priorPrescription
---

## Element: medicationRequest.priorPrescription

**Business Meaning**: An order/prescription that is being replaced AND a link to a resource representing an earlier order related order or prescription.

The published FHIR specifications described this element is slightly different ways in different parts of the FHIR specification;

"*A link to a resource representing an earlier order related order or prescription*" 

and 

"*An order/prescription that is being replaced*".

The following guidance applies to each use case.

### Linking to an earlier order

A medication request that is a repeat of an earlier request would be referenced within **priorPrescription**. This would allow both the ePMA and pharmacy systems to logically link requests and add verification checks to flag any differences to the user.

An order for the same medication but for a different dose can still be linked using **priorPrescription**. In this scenario it would be expected that the prescribing clinician provides [supporting information](develop_medicationrequest_supportinginformation.html) for the pharmacy to confirm the change in the medication request.

### Linking to an order that is being replaced

The medicationRequest being replaced will be referenced within **priorPrescription**. It would be expected that the referenced resource would be updated with a [status](develop_medicationrequest_status.html) of *cancelled*, *entered-in-error* or *stopped*. This will allow both the ePMA and pharmacy systems to make it clear to the human user that one medication request replaces another.
