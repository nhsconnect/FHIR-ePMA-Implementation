---
title: medicationRequest.subject
keywords: design
tags: [design]
sidebar: overview_sidebar
permalink: develop_medicationrequest_subject.html
summary: Implementation guidance for medicationRequest.subject
---

## Element: medicationRequest.subject

**Business Meaning**: A link to a resource representing the person or set of individuals to whom the medication will be given.

The scope of the target use case relates to individual patients only, not groups of patients therefore the linked resource shall only be a FHIR **Patient** resource.

The method by which the Patient resource is linked will be a local implementation decision. There are three options;

 1. Referenced by URL to a FHIR Server
 2. Referenced by an identifier to a Patient resource within the same FHIR Bundle
 3. Referenced by an identifier to a "contained" resource within the medicationRequest resource

FHIR snippets using XML notation are as follows;

    <!-- 1. by URL -->
    <subject>
    	<reference value="https://acmefhirserver/patient/2245386903"/>
    </subject>
    
    <!-- 2. by identifier within the Bundle -->
    <Bundle>
	    <entry>
		    <fullUrl value="patient-2245386903"/>
		    <resource>
			    <Patient>
				    <!-- patient details -->
			    </Patient>
		    </resource>
		</entry>
		<entry>
			<resource>
			    <MedicationRequest>
				    <subject>
					    <reference value="#patient-2245386903"/>
					</subject>
				</MedicationRequest>
			</resource>
		</entry>
    </Bundle>
    
    <!-- 3. by identifier to a contained resource -->
    <MedicationRequest>
	    <contained>
		    <Patient>
			    <id value="patient-2245386903"/>
			    <!-- patient details -->
		    </Patient>
	    </contained>
	    <subject>
		    <reference value="#patient-2245386903"/>
		</subject>
	</MedicationRequest>


[ *CareConnect* ]

CareConnect added a number of extensions to the STU3 Patient resource. The only one relevant to this use case is **identifier (nhsNumber)**. See below for the minimum data set.

[ *STU3* / *R4* ]

Whilst not identical, the elements required to be populated within a **Patient** resource is the same for both versions of FHIR. 

### Minimum Data Set for a Patient Resource

For an implementation using CareConnect, replace **patient.identifier** with the extension specific for use with the NHS Number.
 
- Patient.id = a logical id for the resource
- Patient.identifier.use = "official"
- Patient.identifier.type = "MR"
- Patient.identifier.value = {patient's NHS Number}
- Patient.identifier.period = {any known validity period, omit if unknown}
- Patient.name
- Patient.gender
- Patient.birthDate
- Patient.address

