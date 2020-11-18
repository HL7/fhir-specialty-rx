### Must Support Elements

**Reason for absence is unknown.** If the source system does not have data for a *Must Support* data element, and the reason for absence is unknown:

- The Data Source responding to to a query SHALL NOT include the element in the resource. 

- The Requester SHALL interpret missing data elements within resource instances as data not present in the Data Source system.

**Known reason for absence.** In situations where information on a particular data element is missing and the Data Source knows the precise reason for the absence of data: 

- The Data Source SHALL send the reason for the missing information using values (such as nullFlavors) from the value set where they exist or using the dataAbsentReason extension. *(See next section)*

- The Requester SHALL be able to process resource instances containing data elements asserting missing information.

### Required Elements

If the source system does not have data for a *required* data element (in other words, where the minimum cardinality is greater than 0), participants must follow the rules below.

**Non-Coded Data Elements**. Use the standard FHIR [DataAbsentReason Extension](http://hl7.org/fhir/R4/extension-data-absent-reason.html) in the data type

- Use the code `unknown` - "The value is expected to exist but is not known"
- Example: [Pharmacy Organization lacking a telecom value](Organization-specialty-rx-organization-pharmacy-2-unknown-telecom.html)

**Coded Elements**. 

- *Example, preferred, or extensible* binding strengths (CodeableConcept datatypes)
  - If the source systems has text but no coded data, only the text element is used.
  - If there is neither text or coded data, use the appropriate “unknown” concept code from the value set if available
  - If the value set does not have the appropriate “unknown” concept code, use “unknown” from the  [DataAbsentReason Code System](http://hl7.org/fhir/R4/codesystem-data-absent-reason.html)

- *Required* binding strength (CodeableConcept or code datatypes):

- - Use the appropriate “unknown” concept code from the value set, if available

  - For the following status elements no appropriate “unknown” concept code is available. For these elements, the element cannot be populated as unknown:

  - - `AllergyIntolerance.clinicalStatus`
    - `Condition.clinicalStatus`
    - `DocumentReference.status`
    - `Immunization.status`
    - `Goal.lifecycleStatus`
    - If one of these status codes is missing, t**he Data Source SHALL** respond with a 404 HTTP error code and an OperationOutcome SHALL be returned in response to a query for the resource.

<br />

