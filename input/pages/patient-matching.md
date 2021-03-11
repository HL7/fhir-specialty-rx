The Specialty Rx process supports two exchange patterns, which are described in [Systematic Query Workflows](systematic-queries.html):

- Solicited Model: A pharmacy or other party requests patient information from an EHR or other Data Source
- Unsolicited Model: A Data Source pushes patient data to a recipient proactively when a medication is prescribed--without having received a request

Relating to both of those models, the sections below describe the Data Consumer system's and Data Source system's steps and responsibilities for: 

- identifying / matching the patient   *(solicited model)*
- specifying the desired data   *(solicited model)*
- producing the data   *(solicited and unsolicited models)*
- consuming the data   *(solicited and unsolicited models)*

<p></p>

### Matching Approaches in the Solicited Model

In the *solicited model*, where a pharmacy or other party (Data Consumer system) requests patient information from an EHR or other responder (Data Source system), the Data Consumer system may either...

- **Pre-Match the Patient** and include the Data Source's Patient resource ID in RESTful searches or [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html).

  or

- **Defer Patient Matching** when using the [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html), and include only the Data Consumer system's Patient resource in the request. In this method, patient matching is performed by the Data Source system as a pre-step to creating its response.

<p></p>

### Matching Method One: Patient Pre-Match

Depending on the situation, the Data Consumer system may already have the Data Source's Patient resource (for example, if it received it in a previous FHIR exchange), or it may be in a position to request it using the `Patient/$match` operation.

#### Step 1: Obtain the responder's Patient resource using Patient $match

In this scenario, the Data Consumer system submits a patient match operation against the Data Source's server: 

`URL: [base]/Patient/$match`

*Input parameters.*  In the Specialty Rx process, this request SHALL contain two parameters:

- Patient resource representing the Data Consumer system's patient record
- The `onlyCertainMatches` parameter with the value set to `true`. This prevents the Data Source from returning multiple possible Patient matches.

*Output parameter.*  The `$match` operation returns a Bundle containing...

- the single Patient resource that the Data Source has confidently matched to the Data Consumer system's patient

  or 

- an OperationOutcome resource if the Data Source is unable to return a patient, containing further advice regarding patient selection.

#### Step 2: Populate the patient information in the request

When retrieving information using RESTful searches...
- the Data Consumer system SHALL include a `patient` parameter in the search containing the retrieved patient ID. 

When retrieving information using a Specialty Rx Query message, the Data Consumer system...
- SHALL populate the `requester-patient` parameter with a reference to the **Data Consumer system's Patient resource** 
- SHALL populate the `responder-patient` parameter with the **Data Source's Patient resource**
  - SHALL populate this `responder-patient` Patient resource's `.meta.source` element with the Data Source system's FHIR server URL
- SHALL omit patient references from the query statement(s) contained in the request's `query-string` parameter. *See [Search Conventions](searches.html)*

#### Step 3: Data Source system processes the request

When retrieving information using RESTful searches...
- the Data Source system processes the search according to the standard FHIR conventions, limiting response content to that pertaining to the specified patient. 

When responding to a Specialty Rx Query message...
- Before compiling the response, the Data Source system SHALL verify the patient match referenced in the request's `responder-patient` element.
  - If the match cannot be verified, the Data Source system SHALL return an OperationOutcome describing the error.

<p></p>

### Matching method Two: Deferred Patient Matching (Messaging Only)

In this approach, which applies only to the Specialty Rx Query message, the request contains only the Data Consumer system's Patient resource. The Data Source's Patient resource ID is not referenced in the request.

#### Step 1: Populate the patient information in the Specialty Rx Query message

The Data Consumer system: 

- SHALL populate the `requester-patient` parameter with a reference to the **Data Consumer system's Patient resource** 
- SHALL omit patient references from the query statement(s) contained in the request's `query-string` parameter. *See [Search Conventions](searches.html)*

#### Step 2: Data Source processes the request message

The Data Source system performs patient matching using the request's patient identifying information before compiling the response. The system...

- SHALL locate a match to the responder patient referenced in the request's `requester-patient` parameter.
  - If the Data Source system cannot determine a single, confident match, it SHALL return an OperationOutcome describing the error.
- SHALL append a patient parameter containing the responder's patient ID to each search string supplied in a `query-string` parameter in the request.
  - For example, change the submitted query-string `"Condition"` to `"Condition?patient=EHRPatient123"`.

<p></p>

### Additional Patient Processing Steps for Specialty Rx Messages

#### Populating patient information in response messages (Solicited and Unsolicited)

- In the Specialty Rx Query Response and Query Response - Unsolicited messages, the Data Source system SHALL populate the `responder-patient` element with a reference to the **Data Sources's Patient resource**
- In the Specialty Rx Query Response message, the Data Source system SHALL echo the **Data Consumer's Patient resource** in the `requester-patient` parameter and SHALL populate this Patient resource's `.meta.source` element with the Data Consumer system's FHIR server URL


#### Processing received response messages (Solicited and Unsolicited)

When the Data Consumer system processes a Specialty Rx Query Response or Query Response - Unsolicited message, it...

- *In the Solicited model*
  - SHALL verify that the `requester-patient` parameter contains a reference to the Data Consumer's patient and that its `.meta.source` = Data Consumer system's FHIR server URL
  - SHOULD confirm that the `responder-patient` parameter matches the Data Consumer system's patient
- *In the Unsolicited model* 
  - SHALL match the Patient referenced by the `responder-patient` parameter
  - SHOULD match the MedicationRequest in the `prescription` parameter (including referenced prescribing Practitioner and pharmacy Organization) to the related prescription. The receiving party can handle non-match situations according to their own rules, e.g., accept the message and add the patient to their system after a manual review

<p></p>

### Using the NewRx Medical Record Number in Deferred Matching

The NCPDP NewRx message typically used to transmit new prescriptions in the US does not support inclusion of the patient's FHIR Patient resource ID. 

However, it offers optional patient identifier elements including MedicalRecordIdentificationNumberEHR, which is used to convey the patient's medical record number at the ordering practice.

When received in a NewRx prescription message, Data Consumer systems MAY include the MedicalRecordIdentificationNumberEHR with other patient information transmitted in the `requester-patient` parameter of the Query message. 

Because this identifier is not accompanied by a system URI in the NewRx, implementers SHOULD populate the value in the Patient resource as follows:

- `Patient.identifier.type.coding.system` = "http://terminology.hl7.org/CodeSystem/v2-0203"
- `Patient.identifier.type.coding.code` = "MR"
- `Patient.identifier.type.coding.code.display` = â€œMedical record numberâ€?
- `Patient.identifier.type.text` = â€œMRN from prescriptionâ€?
- `Patient.identifier.value` = [the value received in MedicalRecordIdentificationNumberEHR ]
- `Patient.identifier.system` = [data-absent-reason extension with value "unknown"]

For example:

```
"identifier": [
  {
    "type": {
      "coding": [
        {
          "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
          "code": "MR",
          "display": "Medical record number",
        }
      ],
      "text": "MRN from prescription"
    },
    "_system": {
      "extension": [
        {
          "url": "http://hl7.org/fhir/StructureDefinition/data-absent-reason",
          "valueCode": "unknown"
        }
      ]
    },
    "value": "30455"
  }
]
```

<br/>