---
title: MedicationDispense
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationdispense.html
summary: Initial draft implementation guidance for populating and consuming the FHIR MedicationDispense resource
---

## Introduction

Links to the definitions of the **MedicationRequest** resource within the specifications covered within this guidance.

- MedicationDispense resource within [STU3](https://www.hl7.org/fhir/STU3/medicationdispense.html)
- MedicationDispense resource within [CareConnect](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-MedicationDispense-1)
- MedicationDispense resource within [R4](http://hl7.org/fhir/medicationdispense.html)

## Minimum Viable Product (MVP)

Elements marked as **MVP** denote those recommended to be required for an MVP for the target use case.

### Elements across FHIR Versions

| Element                                                                                   |   MVP   |   STU3   | CareConnect |    R4    |
| :---------------------------------------------------------------------------------------- | :-----: | :------: | :---------: | :------: |
| [`id`](#id)                                                                               | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`identifier`](#identifier)                                                               |  **?**  | &#x2714; |  &#x2714;   | &#x2714; |
| [`partOf`](#partof)                                                                       |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`status`](#status)                                                                       | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`statusReason[x]`](#statusreasonx)                                                       |  **?**  | &#x2716; |  &#x2716;   | &#x2714; |
| [`category`](#category)                                                                   | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`medication[x]`](#medicationx-for-stu3-and-r4-medicationreference-for-careconnect)       | **MVP** | &#x2714; |  &#x2716;   | &#x2714; |
| [`medicationReference`](#medicationx-for-stu3-and-r4-medicationreference-for-careconnect) | **MVP** | &#x2716; |  &#x2714;   | &#x2716; |
| [`subject`](#subject)                                                                     | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`context`](#context)                                                                     |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`supportingInformation`](#supportingInformation)                                         |  **?**  | &#x2714; |  &#x2714;   | &#x2714; |
| [`performer`](#performer)                                                                 | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`location`](#location)                                                                   |         | &#x2716; |  &#x2716;   | &#x2714; |
| [`authorizingPrescription`](#authorizingrescription)                                      | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`type`](#type)                                                                           |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`quantity`](#quantity)                                                                   | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`daysSupply`](#dayssupply)                                                               | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`whenPrepared`](#whenprepared)                                                           | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`whenHandedOver`](#whenhandedover)                                                       |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`destination`](#destination)                                                             | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`receiver`](#receiver)                                                                   |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`note`](#note)                                                                           | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`dosageInstruction`](#dosageinstruction)                                                 | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`substitution`](#substitution)                                                           | **MVP** | &#x2714; |  &#x2714;   | &#x2714; |
| [`detectedIssue`](#detectedissue)                                                         |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`notDone`](#notdone)                                                                     |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`notDoneReason[x]`](#notdonereasonx)                                                     |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`eventHistory`](#eventhistory)                                                           |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`meta`](#meta)                                                                           |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`implicitRules`](#implicitrules)                                                         |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`language`](#language)                                                                   |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`text`](#text)                                                                           |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`contained`](#contained)                                                                 |         | &#x2714; |  &#x2714;   | &#x2714; |
| [`modifierExtension`](#modifierextension)                                                 |         | &#x2714; |  &#x2714;   | &#x2714; |

## Medication Dispense Elements

### id

| **Date Type:** | `Id` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/datatypes.html#id), [`R4`](http://hl7.org/fhir/datatypes.html#id) |

The logical id of the resource, as used in the URL for the resource. Once assigned, this value never changes.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### identifier

| **Date Type:** | `Identifier` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/datatypes.html#Identifier), [`R4`](http://hl7.org/fhir/datatypes.html#Identifier) |

External IDs for this request. Identifiers associated with this medication request that are defined by business processes and/or used to refer to it when a direct URL reference to the resource itself is not appropriate. They are business identifiers assigned to this resource by the performer or other systems and remain constant as the resource is updated and propagates from server to server.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### partOf

| **Date Type:** | `Reference(Procedure | CareConnect-Procedure-1)` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.partOf), [`CareConnect`](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-MedicationDispense-1), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.partOf) |

The procedure that the dispense is done because of.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### status

| **Date Type:** | `Code` |
| **Required / Cardinality** | `Required (STU3/CareConnect) 0..1`, `Mandatory (R4) 1..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/datatypes.html#code), [`R4`](http://hl7.org/fhir/datatypes.html#code) |

The cardinality of status has been changed from 0..1 in STU3 to 1..1 in R4.

When used it must be populated with a fixed value set defined within the FHIR standard.

It is expected that most implementations will require the use of status to support workflow.

**Note** The value sets between [`STU3/CareConnect`](http://hl7.org/fhir/stu3/valueset-medication-dispense-status.html) and [`R4`](http://hl7.org/fhir/valueset-medicationdispense-status.html) differ, and an example workflow and interpretation of these statuses is yet to be defined.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### statusReason[x]

| **Date Type:** | `CodeableConcept | Reference(DetectedIssue)` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.statusReason_x_) |

This could be used; however, it is only compatible with R4.

At this time, it is **unknown** as to whether this should be included as part of the MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### category

| **Date Type:** | `CodeableConcept` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.category), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.category) |

Indicates the type of medication dispense (for example, where the medication is expected to be consumed or administered (i.e. inpatient or outpatient)).

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### medication[x] for STU3 and R4, medicationReference for CareConnect

| **Date Type:** | `CodeableConcept | Reference(Medication)` |
| **Required / Cardinality** | `Mandatory 1..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.medication_x_), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.medication_x_) |

Where the requested medication is contained within the NHS dm+d then it must be recorded using the dm+d standard. Implementation is recommended to be via a referenced [Medication](develop_medication.html) resource.

See the [Overview](develop_overview.html#using-fhir-references) page for guidance on using FHIR References.

**Note**: At the time of writing an alpha implementation of a dm+d FHIR Medication Resource Server is available from the North East CSU as a [demonstrator](https://dmdsite-uks-test-web.azurewebsites.net) and associated [API](https://apidmd001.azurewebsites.net/index.html).

It is recommended that the `medicationReference.display` is populated with the medication description as selected by the clinician. This may be slightly different to the medication described as returned by a SNOMED/dm+d terminology FHIR server if the ePMA system has not fully implemented dm+d into their medication picking list.

#### Requested medication with no dm+d code

Medication not published within the dm+d may be requested in the Acute care setting. In this scenario it is recommended to use the **CodeableConcept** variant for this element. Software logic can then clearly distinguish this from nationally coded dm+d medication.

If the ePMA system has both a locally assigned code and description for the medication then;

- The `medicationCodeableConcept.text` should be the description for the medication.
- The `medicationCodeableConcept.coding.code` should be the code for the medication.
- The `medicationCodeableConcept.coding.display` should be the description for the medication, i.e. the same value as `medicationCodeableConcept.text`.

If the ePMA system only has a description for the medication then;

- The `medicationCodeableConcept.text` should be the locally assigned description for the medication.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### subject

| **Date Type:** | `Reference(Patient | Group | CareConnect-Patient-1 )` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.subject), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.subject) |

See the [Overview](develop_overview.html#using-fhir-references) page for guidance on using FHIR References.

**Note**: It is acknowledged that a typical Hospital Patient Administration System (PAS) available today will not expose a FHIR interface so referencing by URL will most likely not be available for some time. However this should be a target architecture so that the FHIR-enabled PAS can be used as a trusted source of Patient resources across multiple hospital systems.

See population of a [Patient](develop_patient.html) resource.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### context

| **Date Type:** | `Reference(Encounter | EpisodeOfCare | CareConnect-EpisodeOfCare-1)` |
| **Required / Cardinality** | `Required 0..1`, |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.context), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.context) |

The encounter or episode of care that establishes the context for this event.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### supportingInformation

| **Date Type:** | `Reference(Any | Resource)` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.supportingInformation), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.supportingInformation) |

Additional information that supports the medication being dispensed.

At this time, it is **unknown** as to whether this should be included as part of the MVP.

**Note** This can link to any FHIR resource - could this be used for financial information (e.g. cost centres)?

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### performer

| **Date Type:** | `BackboneElement` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.performer), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.performer) |

Indicates who performed the event - e.g. the person the dispensed the medication.
It's likely that the recipient will want to know this information,

This is most likely going to be a UK Core Practitioner Role (GPhC registration) as Organisation on its own is not specific enough.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### location

| **Date Type:** | `BackboneElement` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.location) |

The principal physical location where the dispense was performed.

For primary care this will likely be business required; however, is this needed for secondary care?

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### authorizingPrescription

| **Date Type:** | `Reference(MedicationRequest | CareConnect-MedicationRequest-1 )` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.authorizingPrescription), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.authorizingPrescription) |

A reference to the original medication request.

FHIR guidance states optional; however, this should be mandatory for any implementation within England.

Refer to the [medicationRequest](develop_medicationrequest.html) implementation guidance for more information.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### type

| **Date Type:** | `CodeableConcept` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.type), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.type) |

Indicates the type of dispensing event that is performed. For example, Trial Fill, Completion of Trial, Partial Fill, Emergency Fill, Samples, etc.

This will most likely be a type of `prescription-dispensing` - could it be used for anything else?

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### quantity

| **Date Type:** | `SimpleQuantity` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.quantity), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.quantity) |

The amount of medication that has been dispensed. Includes unit of measure.

Prefer both product and dose based quantity should be included for readability.

For example: _insert example here_

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### daysSupply

| **Date Type:** | `SimpleQuantity` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.daysSupply), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.daysSupply) |

The amount of medication expressed as a timing amount.

This could be tricky as may not always be able to provided - e.g. _"use when required"_ indicates that usage is optional, and may not be able to be calculated.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### whenPrepared

| **Date Type:** | `dateTime` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.whenPrepared), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.whenPrepared) |

The time when the dispensed product was packaged and reviewed.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### whenHandedOver

| **Date Type:** | `dateTime` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.whenHandedOver), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.whenHandedOver) |

The time the dispensed product was provided to the patient or their representative.

This could be a useful component to capture; however, it is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### destination

| **Date Type:** | `Reference(Location | CareConnect-Location-1)` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.destination), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.location) |

The principal physical location where the dispense was performed.

It is assumed that this will be useful, hence suggested in the MVP; however, what would it be used for?

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### receiver

| **Date Type:** | `Reference(Patient | Practitioner | CareConnect-Patient-1 | CareConnect-Practitioner-1)` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.receiver), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.receiver) |

Identifies the person who picked up the medication. This will usually be a patient or their caregiver, but some cases exist where it can be a healthcare professional.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### note

| **Date Type:** | `Annotation` |
| **Required / Cardinality** | `Required 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.note), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.note) |

Extra information about the dispense that could not be conveyed in the other attributes.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### dosageInstruction

| **Date Type:** | `Dosage` |
| **Required / Cardinality** | `Required 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.dosageInstruction), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.dosageInstruction) |

A required business element for all MVP implementations.

Population of just the `dosageInstruction.text` element would be unacceptable for a successful implementation.

Refer to [FHIR Dose Syntax Implementation Guidance](https://developer.nhs.uk/apis/dose-syntax-implementation/) (or any subsequent version) for guidance.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### substitution

| **Date Type:** | `BackboneElement` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.substitution), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.substitution) |

Indicates whether or not substitution was made as part of the dispense. In some cases, substitution will be expected but does not happen, in other cases substitution is not expected but does happen. This block explains what substitution did or did not happen and why. If nothing is specified, substitution was not done.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### detectedIssue

| **Date Type:** | `Reference(DetectedIssue)` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.detectedIssue), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.detectedIssue) |

Indicates an actual or potential clinical issue with or between one or more active or proposed clinical actions for a patient; e.g. drug-drug interaction, duplicate therapy, dosage alert etc.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### notDone

| **Date Type:** | `boolean` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.notDone) |

The default value of a boolean is `false`.

Set to `true` if the dispense was not performed for some reason.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### notDoneReason[x]

| **Date Type:** | `CodeableConcept | Reference(DetectedIssue)` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.notDone) |

Indicates the reason why a dispense was not performed.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### eventHistory

| **Date Type:** | `Reference(Provenance)` |
| **Required / Cardinality** | `Optional 0..*` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.detectedIssue), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.eventHistory) |

A summary of the events of interest that have occurred, such as when the dispense was verified.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### meta

| **Date Type:** | `Meta` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.meta), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.meta) |

The metadata about the resource. This is content that is maintained by the infrastructure. Changes to the content may not always be associated with version changes to the resource.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### implicitRules

| **Date Type:** | `Uri` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.implicitRules), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.implicitRules) |

A reference to a set of rules that were followed when the resource was constructed, and which must be understood when processing the content.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### language

| **Date Type:** | `Code` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.language), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.language) |

The base language in which the resource is written.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### text

| **Date Type:** | `Narrative` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.text), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.text) |

A human-readable narrative that contains a summary of the resource, and may be used to represent the content of the resource to a human. The narrative need not encode all the structured data, but is required to contain sufficient detail to make it "clinically safe" for a human to just read the narrative. Resource definitions may define what content should be represented in the narrative to ensure clinical safety.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### contained

| **Date Type:** | `Resource` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.contained), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.contained) |

These resources do not have an independent existence apart from the resource that contains them - they cannot be identified independently, and nor can they have their own independent transaction scope.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}

### modifierExtension

| **Date Type:** | `Extension` |
| **Required / Cardinality** | `Required 0..1` |
| **Version Support** | [`STU3 / CareConnect`](https://www.hl7.org/fhir/STU3/medicationdispense-definitions.html#MedicationDispense.modifierExtension), [`R4`](http://hl7.org/fhir/medicationdispense-definitions.html#MedicationDispense.modifierExtension) |

May be used to represent additional information that is not part of the basic definition of the resource, and that modifies the understanding of the element that contains it. Usually modifier elements provide negation or qualification. In order to make the use of extensions safe and manageable, there is a strict set of governance applied to the definition and use of extensions.

Though any implementer is allowed to define an extension, there is a set of requirements that SHALL be met as part of the definition of the extension. Applications processing a resource are required to check for modifier extensions.

It is recommended this element is **not implemented** as part of an MVP.

[top of page](develop_medicationdispense.html){: .btn .btn-default .btm-sm}
