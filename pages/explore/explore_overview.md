---
title: Explore Overview
keywords: explore, design, reference
tags: [design,explore]
sidebar: overview_sidebar
permalink: explore_overview.html
summary: An overview of this implementation guidance.
---

## Structure of this Guidance

This guidance document provides background information on the target ePMA to pharmacy system use case within this **Explore** section.

Guidance for the use of each element of the MedicationRequest FHIR resource is provided within the **Develop** section.

## What is an Electronic Prescribing and Medicines Administration (ePMA) System?

An ePMA system is used to "*facilitate and enhance communication of a prescription or medicine order, aiding the choice, administration and supply of a medicine through knowledge and decision support and providing a robust audit trail for the entire medicines use process*".

Definition taken from “*Safer Hospitals, Safer Wards: Achieving an Integrated Digital Care Record*”, published by NHS England, 2013.

## What is a Hospital Pharmacy System?

A hospital pharmacy system supports the provision of medicines across a hospital. It will typically be based around medicine stock control functionality. It can print medication labels. Most will have elements of a patient medication record and support the safe dispensing of medicines through knowledge and decision support.

## What is the Interoperability Requirement?

The sharing of data between the ward and hospital pharmacy is for the purpose of medicines supply. The implementation of ePMA systems within UK hospitals continues to grow but many still operate with paper-based processes. Many of these paper-based processes require repeated stages of human interpretation of hand-written medicine order forms, and re-keying of medicine orders. For those who have implemented ePMA systems, there is no established interoperability standard between the ePMA system and hospital pharmacy systems.

The interoperability requirement is to send or share an electronic medication order / prescription entered into the ePMA system, with the hospital pharmacy system.

![Status Transitions](images/interop_diagram.jpg)

### RESTful Implementations

In a RESTful implementation, it is recommended that the MedicationRequest is POSTed to the pharmacy system using an HTTP POST operation. Here, the pharmacy system is acting as the FHIR server.

In a RESTful implementation, it is recommended that any update to an existing MedicationRequest is PATCHed to the pharmacy system using an HTTP PATCH operation. A PATCH operation sends just the changed elements of the resource to the FHIR server. It is an alternative to updating an entire resource using an HTTP PUT. Using a PUT requires more data bandwidth but is also a simpler solution so is also an acceptable solution.

A further alternative for the pharmacy system to obtain updates to MedicationRequest resources is to query the ePMA system with a GET operation. The design challenge here is knowing when to query. A polling approach would be inefficient unless updates are occurring frequently to individual resources. The ePMA system could notify the pharmacy in some way to trigger a query/GET operation. This is obviously a two-step operation (notification followed by a GET) instead of the single-step operation implemented with a PATCH (or PUT).

Refer to the [STU3 FHIR RESTful standards](http://hl7.org/fhir/STU3/http.html#update) and [R4 FHIR RESTful standards](https://hl7.org/fhir/R4/http.html) for more information.

### Dispensing and Administration Events

The scope of this version of implementation guidance  excludes the reverse interaction; a send or share of an electronic dispensing event entered into the hospital pharmacy system, with the ePMA system, using the **MedicationDispense** FHIR resource. 

The scope of this version of implementation guidance excludes the sharing of medication administration events between systems using the **MedicationAdministration** FHIR resource. 

These will be added in a future versions of this guidance.

## Medication orders within UK ePMA systems and how they are supported with FHIR

Typically within UK hospitals, ePMA systems support two types of medication request (or order);

 1. Initial medication request
 2. Re-Supply of a previous medication request

### Initial Medication Request

An "Initial Medication Request" is the first time a request for a medicine is made for a patient. This can include a long term medicine or an acute medicine for a specified duration. Each request shall be for one medication. The structured dosage instruction shall specify the administration requirement, e.g. “50mg daily with food”, and any time or dosing bounds, e.g. “for 7 days”, all represented in the structured and machine readable FHIR [dosage](develop_medicationrequest.html#dosageinstruction) structure.

Most ePMA medication requests are deemed to be on-going unless specifically stated within the dosage instruction with date, time or dose bounds. Where no end criteria is specified the hospital pharmacy will typically dispense a quantity of medication as per their local agreed best practice. For example, sufficient medication for a given number of days, depending on how frequently the ward and pharmacy want to re-order medication. When more medication is required, a "Re-fill Medication Request" should be submitted.

### Re-Supply Medication Request

When a patient requires a re-supply of the same medication as previously ordered.

For a minimum viable product (MVP) implementation it is recommended to reference a previous MedicationRequest using the [priorPrescription](develop_medicationrequest.html#priorprescription) element. This can either reference the last MedicationRequest or the first MedicationRequest. This choice can be a local implementation decision. Note that the FHIR standard also allows a previous supply to be reference using the [basedOn](develop_medicationrequest.html#basedOn) element. For this guidance it is recommended **basedOn**, if used, it used to reference a **CarePlan** resource. 

It is recommended that a re-supply should;
- only be made against a previous order that has a [status](develop_medicationrequest.html#status) of `active` or `complete`
- be identical to the previous supply with regard to the [medication](develop_medicationrequest.html#medicationx) and [dosageInstruction](develop_medicationrequest.html#dosageInstruction)
- allow a different [requester](develop_medicationrequest.html#requester) and/or [recorder](develop_medicationrequest.html#recorder) to the previous supply
- allow a different [dispenseRequest](develop_medicationrequest.html#dispenseRequest) (if implemented within the system) to the previous supply to cater for the scenario where a re-supply is required for a certain number of days or quantity of medication. For example, a final supply prior to the end of the treatment or course or before the patient is to be discharged.
