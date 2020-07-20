#### <br>Constrains US Core Condition

The Specialty Rx Condition profile is based on US Core Condition. 

*Note: Development of this profile is in process. At this stage, it does not contain constraints beyond the base US Core profile. If the workgroup determines that the US Core profile can be used as-is, this profile will be removed from the implementation guide.*

<br>

#### Mandatory Search Parameters

In order to respond to Specialty Rx data requests, the following search parameters and search parameter combinations SHALL be supported.:

1. **SHALL** support searching for all allergies for a patient using the **[`patient`](https://www.hl7.org/fhir/us/core/SearchParameter-us-core-allergyintolerance-patient.html)** search parameter:

   ```
   GET [base]/AllergyIntolerance?patient=[reference]
   ```

   <br>


