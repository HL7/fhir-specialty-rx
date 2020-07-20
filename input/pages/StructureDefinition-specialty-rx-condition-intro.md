#### <br>Constrains US Core Condition

The Specialty Rx Condition profile is based on US Core Condition. It modifies it by constraining the code systems allowed in the Condition.code element, removing ICD-9-CM from the US Core Condition Code.

<br>

#### Mandatory Search Parameters

In order to respond to Specialty Rx data requests, the following search parameters and search parameter combinations SHALL be supported.:

1. **SHALL** support searching for all conditions including problems, health concerns, and encounter diagnosis for a patient using the **[`patient`](https://www.hl7.org/fhir/us/core/SearchParameter-us-core-condition-patient.html)** search parameter:

   `GET [base]/Condition?patient=[reference]`

   <br>


