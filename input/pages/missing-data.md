### Elements Specified as *Must Support*

Profiles in this guide specify certain elements as "Must Support". These SHALL be interpreted as follows:

- Data Source Systems SHALL be capable of populating each Must Support data element when sharing the resource in an exchange defined in this guide. It must be capable of both *possessing the data* for the element and *exchanging* it.

- Requesting Systems SHALL be capable of processing received instances containing the Must Support data elements without generating an error or causing the application to fail.

- If the Must Support element is specified as required (minimum cardinality of 1 or higher), the element SHALL be present in the instance and SHALL have a value unless the profile is defined in U.S. Core or based on it \*, in which case a `dataAbsentReason` extension may be sent in place of the value.

  *\* Profiles defined in this guide that are based on US Core are [Specialty Rx Patient](StructureDefinition-specialty-rx-patient.html), [Specialty Rx Medication Request](StructureDefinition-specialty-rx-medicationrequest.html),  [Specialty Rx Organization Pharmacy](StructureDefinition-specialty-rx-organization-pharmacy.html) and [Specialty Rx Practitioner](StructureDefinition-specialty-rx-practitioner.html). These are used solely in the Specialty Rx messages.*

- Requesting Systems SHALL interpret missing elements in received resources as data that is either not present in the Data Source System or not shareable with the Requesting System for privacy or other reasons.

- Requesting Systems SHALL be able to process resource instances containing data elements containing `dataAbsentReason` extensions in place of values where allowed as described here.

<p></p>

### Handling Missing Data

#### In Must Support Elements

**Unknown Reason.** If the source system does not have data for a *Must Support* data element, and the reason for absence is unknown:

- The Data Source responding to a query SHALL NOT include the element in the resource. 

- The Requester SHALL interpret missing data elements within resource instances as data not present in the Data Source system.

**Known Reason.** In situations where information on a particular data element is missing and the Data Source knows the precise reason for the absence of data: 

- The Data Source SHALL send the reason for the missing information using values (such as nullFlavors) from the value set where they exist or using the dataAbsentReason extension. *(See next section)*

- The Requester SHALL be able to process resource instances containing data elements asserting missing information.

#### In Required Elements

If the source system does not have data for a *required* data element (in other words, where the minimum cardinality is greater than 0), participants must follow the rules below.

**Non-Coded Data Elements**. Use the FHIR [DataAbsentReason Extension](http://hl7.org/fhir/R4/extension-data-absent-reason.html) with the code, `unknown`, which means *the value is expected to exist but is not known*.

- Example: [Pharmacy Organization lacking a telecom value](Organization-specialty-rx-organization-pharmacy-2-unknown-telecom.html)

**Coded Data Elements** 

- ***Example, preferred, or extensible* binding strengths**
  
  - If the source systems has text but no coded data, only the text element is used.
  - If there is neither text nor coded data, use the appropriate “unknown” concept code from the value set if available
  - If the value set does not have the appropriate “unknown” concept code, use “unknown” from the  [DataAbsentReason Code System](http://hl7.org/fhir/R4/codesystem-data-absent-reason.html)
  
- ***Required* binding strength** 

    - Use the appropriate “unknown” concept code from the value set, if available. 
    - In cases where the Data Source does not know the correct code, and the value set lacks an appropriate "unknown" code, it SHALL respond to a query for the resource with an OperationOutcome accompanied by a 404 HTTP error code. 
    
    For example, the following status elements do not contain an “unknown” concept code--and so, the element cannot be populated as unknown:
    
    - AllergyIntolerance.clinicalStatus
    - Condition.clinicalStatus
    - DocumentReference.status

<p></p>

### Conformance to US Core Profiles

Resources returned in required and recommended searches defined in [Search Conventions](searches.html) SHALL conform to the associated US Core profiles as outlined in [US Core Profiles](us-core-profiles.html).

Further, when other resources not profiled in this implementation guide are exchanged as part of a Specialty Rx workflow (for example, other resource types returned in response to a Specialty Rx Query message), they SHOULD conform to US Core profiles where applicable profiles exist.

<br />

