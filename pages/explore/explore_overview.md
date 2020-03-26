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

Guidance for the use of each element of the medicationRequest FHIR resource is provided within the **Develop** section.

## What is an Electronic Patient Medication Administration (ePMA) System?

An ePMA system is used to "*facilitate and enhance communication of a prescription or medicine order, aiding the choice, administration and supply of a medicine through knowledge and decision support and providing a robust audit trail for the entire medicines use process*".

Definition taken from “*Safer Hospitals, Safer Wards: Achieving an Integrated Digital Care Record*”, published by NHS England, 2013.

## What is an Hospital Pharmacy System?

A hospital pharmacy system supports the provision of medicines across a hospital. It will typically be based around medicine stock control functionality. It can print medication labels. Most will have elements of a patient medication record and support the safe dispensing of medicines through knowledge and decision support.

## What is the Interoperability Requirement?

The implementation of ePMA systems within UK hospitals continues to grow but many still operate with paper-based processes. Many of these paper-based processes require repeated stages of human interpretation of hand-written medicine order forms, and re-keying of medicine orders. For those who have implemented ePMA systems, there is no established interoperability standard between the ePMA system and hospital pharmacy systems.

The interoperability requirement is to send or share an electronic medication order (aka a prescription) entered into the ePMA system, with the hospital pharmacy system.

![Status Transitions](images/interop_diagram.jpg)

The scope of this version of implementation guidance  excludes the reverse interaction; a send or share an electronic dispensing event entered into the hospital pharmacy system, with the ePMA system. This will be added in a future version of this guidance.
