---
title: medicationRequest.id
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_id.html
summary: Implementation guidance for medicationRequest.id
---

## Element: medicationRequest.id

**Business Meaning**: Unique logical identifier for the resource.

### Logical Identifier Creation

It is highly recommended that the logical id value is a Universally Unique Identifier (UUID) using a standard UUID generator available in most programming languages.

The most comprehensive current definition of the logical id is within the FHIR [R4](https://hl7.org/fhir/R4/resource.html#Resource) standard. The key phrase from the FHIR standard is the logical id is "...*assigned by the server responsible for storing it*".

Vendors have advised that there could be several different scenarios where a MedicationRequest could be stored and it is an implementation decision about where the master MedicationRequest should reside. Possible scenarios for the master MedicationRequest location include;
-   ePMA system FHIR Server
-   Dispensing system FHIR Server
-   Centrally hosted FHIR server (inside hospital network)
-   Centrally hosted FHIR server (cloud hosted) **Note**: This would be the scenario when the NHS Electronic Prescription Service implements the FHIR standard.

A further implementation decision is who creates the logical id.
-   **Server**:  If the hosting system creates the logical id then the client system would send the MedicationRequest (without an id) as a REST POST command. The created logical id should always be included within the HTTP 201 response so the client can persist this id. For centrally hosted FHIR servers it should always be the hosting system the creates the id so that the server can be responsible for logical id uniqueness.
-   **Client**:  If the client system creates the logical id then the client system would send the MedicationRequest (with an id) as a REST PUT command. The REST PUT command will update a record, but if it does not exist create a new record. This is in line with the [STU3 FHIR RESTful standards](http://hl7.org/fhir/STU3/http.html#update) and [R4 FHIR RESTful standards](https://hl7.org/fhir/R4/http.html). If the client system sends the MedicationRequest resource via an asynchronous interoperability pattern then the logical id must be populated with a UUID by the client system. An example would be sending a MedicationRequest within a FHIR payload via the NHS Digital MESH platform.

### Additional Business Identifiers
If either a client or server wants to use an additional business identifier this would be added as an MedicationRequest.identifier and the minimum requirement is:
-   A system value: defining the source of the system it has come from
-   A value: giving the identifier value

### Handling Duplicate Logical Identifiers

If a client system creates the logical id and there are multiple clients sending MedicationRequests there is a possibility a duplicate logical id occurs. In this event the duplicate id (the second code received) will be rejected with a response stating the logical id is duplicated. The requesting system will need to send the request again with a new logical identifier.

For this reason, within an implementation where multiple clients are POSTing to a FHIR server, it is highly recommenced that the FHIR server creates the logical id to remove the risk of duplication.

