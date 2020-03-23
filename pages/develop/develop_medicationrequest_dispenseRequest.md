---
title: Element: dispenseRequest
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_dispenserequest.html
summary: Implementation guidance for medicationRequest.dispenseRequest
---

## Element: medicationRequest.dispenseRequest ##

**Business Meaning**: Information related to the dispensing of the medication.

[ [STU3] | [R4] ]

Refer to https://developer.nhs.uk/apis/dose-syntax-implementation-1-3-1-alpha/index.html (or any subsequent version).

Many elements within this structure are to support primary care prescribing processes using VMP and AMP dm+d concepts and where a structured dosage instruction is not populated.

It is recommended that this structure is omitted, unless required data to be shared cannot be appropriately populated elsewhere within the resource.
