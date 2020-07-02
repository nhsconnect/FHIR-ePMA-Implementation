---
title: Error handling
keywords: fhir, development, operation outcome, error
tags: [fhir,development,error]
sidebar: overview_sidebar
permalink: develop_errorhandling.html
summary: Implementation guidance for error handling
---

The error handling approach defined below follows the approach implemented within GPConnect and the Spine Core FHIR API Framework, based on FHIR STU3.

Guidance for error handling within a FHIR R4 implementation may differ. Refer to [FHIR R4 UK Core](https://simplifier.net/UKCore) documentation when available.

## Operation outcome usage

When a RESTful interaction or operation fails an **OperationOutcome** resource is used to convey specific detailed processable error information back to the client as part of the HTTP response.

In the event of an error, provider systems **SHALL** respond by providing an OperationOutcome resource profiled to [Spine-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1).

The `Spine-OperationOutcome-1`:
- **SHALL** contain a definition of severity in the `OperationOutcome.issue.severity` field providing a value from the [valueset-issue-severity](http://hl7.org/fhir/STU3/valueset-issue-severity.html) value set. In all cases described in this guidance, the value used will be `error`.
- **SHALL** contain a definition of the type of error in the `OperationOutcome.issue.code` element, providing a value from the [issue-type](http://hl7.org/fhir/STU3/valueset-issue-type.html) value set.
- **SHALL** contain details of the `Spine error code` in the `OperationOutcome.issue.details.coding.code` and `OperationOutcome.issue.details.coding.display` fields. These shall be taken from the standard set of NHS Spine error codes as defined in the [spine-error-or-warning-code-1](https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1) value set. The Spine error and warning codes provide a greater degree of error handling granularity, and also ensure a standardised error handling approach across NHS APIs.
- **SHOULD** provide additional diagnostic details of the error in the `OperationOutcome.diagnostics` property where such details securely provide additional error context for consumer applications. Patient identifiable data should not be included within this property.


The sections below provide guidance on the error details to be returned in a number of key scenarios.

### Identity validation errors ####

Provider systems **SHALL** respond by returning one of the following `OperationOutcome` error codes where FHIR resource identity error scenarios are encountered:

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | -----------|------------|-------------|
| `400`     | value | INVALID_IDENTIFIER_SYSTEM | Invalid identifier system |
| `400`     | value | INVALID_IDENTIFIER_VALUE | Invalid identifier value |
| `400`     | value | INVALID_NHS_NUMBER   | NHS number invalid |
| `404`     | not-found | ORGANISATION_NOT_FOUND   | Organisation record not found |
| `404`     | not-found | PATIENT_NOT_FOUND   | Patient record not found |
| `404`     | not-found | PRACTITIONER_NOT_FOUND   | Practitioner record not found |
| `404`     | not-found | NO_RECORD_FOUND | No record found |

#### Example: Invalid NHS number supplied #####

If an invalid NHS number value is supplied the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "value",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "INVALID_NHS_NUMBER",
            "display": "Invalid NHS number"
          }
        ]
      }
    }
  ]
}
```

#### Example: Patient not found #####

For example, if a valid NHS number value is supplied but no local record exists for that patient, then the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "not-found",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "PATIENT_NOT_FOUND",
            "display": "Patient not found"
          }
        ]
      }
    }
  ]
}
```

### Security validation errors ###

When a client system does not present correct security parameters, provider systems **SHALL** return one of the following `OperationOutcome` details: 

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | -----------|------------|-------------|
| `403` | forbidden | ACCESS_DENIED | Access denied |


#### Example: Access denied #####

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "forbidden",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "ACCESS_DENIED",
            "display": "Access denied"
          }
        ]
      },
      "diagnostics": "Invalid authorisation token."
    }
  ]
}
```

### Duplicate errors ###

When responding to consumer API requests, provider systems **SHALL** return one of the following `OperationOutcome` details when a resource could not be created or updated because it would cause a duplicate in the provider system:

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | -----------|------------|-------------|
| `409` | duplicate | DUPLICATE_REJECTED | Create would lead to creation of a duplicate resource |


For example, if the ePMA system attempted to send a MedicationRequest that is already an active record on the pharmacy system the error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "duplicate",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "DUPLICATE_REJECTED",
            "display": "Create would lead to creation of duplicate resource"
          }
        ]
      },
      "diagnostics": "MedicationRequest record already exists with that logical identifier"
    }
  ]
}
```

### Resource validation errors ###

Where FHIR resource validation issues arise during processing of consumer requests, provider systems **SHALL** utilise one the following error details:

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | ---------- | ---------- | ----------- |
| `422`     | invalid | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | invalid | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | invalid | REFERENCE_NOT_FOUND | Referenced resource not found. |


Detailed diagnostic information **MUST** be supplied when erroring on the codes above.

INVALID_PARAMETER would be used in the following, or similar, scenarios:
- An invalid date/time value specified in a custom operation parameter.

INVALID_RESOURCE would be used in situations such as the following:
- Resource fails structural validation.
- A resource fails to be processed because of a FHIR constraint, or other rule application, where the error is not already covered by other error codes

REFERENCE_NOT_FOUND describes a scenario where a consumer POSTs a FHIR resource which contains a FHIR reference that cannot be found. 

#### Example: Reference not found #####

For example, if a MedicationRequest referenced a Practitioner resource that could not be found or resolved by the server. The following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invalid",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "REFERENCE_NOT_FOUND",
            "display": "FHIR reference not found"
          }
        ]
      },
      "diagnostics": "Referenced Practitioner resource not found"
    }
  ]
}
```

### Malformed request errors ###

When the server cannot or will not process a request due to an apparent client error then the following `BAD_REQUEST` error **SHALL** be used to return debug details.

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | ---------- | ---------- | ----------- |
| `400`     | invalid | BAD_REQUEST | Submitted request is malformed/invalid. |


BAD_REQUEST Spine error codes should be used in the following types of scenario:
- JWT claims information is not valid JSON, is null, or has an invalid value 
- invalid FHIR resource in JWT claim (for example, Patient resource when Practitioner expected)
- malformed JSON or XML content in request body
- an expected header is missing or invalid
- invalid HTTP verb used

#### Example: Malformed JSON Web Token in request #####

For example, if the request contained a null claim within a JSON Web Token (JWT), then the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invalid",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "BAD_REQUEST",
            "display": "Bad request"
          }
        ]
      },
      "diagnostics": "Malformed JWT"
    }
  ]
}
```



### Internal server errors ###

When the FHIR server has received a request for an operation or FHIR resource which is not (yet) implemented, then the NOT_IMPLEMENTED Spine error code **SHALL** be used.

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | ---------- | ---------- | ----------- |
| `501`     | not-supported | NOT_IMPLEMENTED | FHIR resource or operation not implemented at server |


When the error is **unexpected** and the server can't be more specific on the exact nature of the problem then the `INTERNAL_SERVER_ERROR` Spine error code **SHALL** be used, and diagnostics **SHALL** be included to provide detail of the error.

| HTTP code | Issue type | Error code - code | Error code - display |
| --------- | ------- | ---------- | ----------- |
| `500`     | processing | INTERNAL_SERVER_ERROR | Unexpected internal server error. |

#### Example: Unexpected exception #####

For example, if an unexpected internal exception is thrown by either an Operation or RESTful API, then the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "exception",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "INTERNAL_SERVER_ERROR",
            "display": "Internal server error"
          }
        ]
      },
      "diagnostics": "Any further internal debug details i.e. stack trace details etc."
    }
  ]
}
```
