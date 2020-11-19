The Specialty Rx process supports two exchange patterns, which are described in [Systematic Query Workflows](systematic-queries.html):

- Solicited Model: A pharmacy or other party requests patient information from an EHR or other data source
- Unsolicited Model: A data source pushes patient data to a recipient proactively when a medication is prescribed--without having received a request

Relating to both of those models, the sections below describe the requester's and data source's steps and responsibilities for: 

- identifying / matching the patient   *(solicited model)*
- specifying the desired data   *(solicited model)*
- producing the data   *(solicited and unsolicited models)*
- consuming the data   *(solicited and unsolicited models)*

<br>

### Matching Approaches: Pre-Match and Deferred

In the *solicited model*, where a pharmacy or other party (Requesting System) requests patient information from an EHR or other responder (Data Source System), the Requesting System may either...

- **Pre-Match the Patient** and include the Data Source's Patient resource ID in RESTful searches or [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html).

  or

- **Defer Patient Matching** when using the [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html), and include only the Requesting System's Patient resource in the request. In this method, patient matching is performed by the Data Source System as a pre-step to creating its response.

<br>

### Matching Method One: Patient Pre-Match

Depending on the situation, the Requesting System may already have the Data Source's Patient resource (for example, if it received it in a previous FHIR exchange), or it may need to request it using the `Patient/$match` operation.

#### Step 1: Obtain the responder's Patient resource using Patient $match

In this scenario, the Requesting System submits a patient match operation against the Data Source's server: 

`URL: [base]/Patient/$match`

*Input parameters.*  In the Specialty Rx process, this request SHALL contain two parameters:

- Patient resource representing the requester's patient record
- The `onlyCertainMatches` parameter with the value set to `true`. This prevents the responder from returning multiple possible Patient matches.

*Output parameter.*  The `$match` operation returns a Bundle containing...

- the single Patient resource that the responder has confidently matched to the requester's patient

  or 

- an OperationOutcome resource if the responder is unable to return a patient, containing further advice regarding patient selection.

#### Step 2: Populate the patient information in the request

When retrieving information using RESTful searches...
- the Requesting System SHALL include a `patient` parameter in the search containing the retrieved patient ID. 

When retrieving information using a Specialty Rx Query message, the Requesting System...
- SHALL populate the `requester-patient` parameter with a reference to the **Requesting System's Patient resource** 
- SHALL populate the `responder-patient` parameter with the **Data Source's Patient resource**
  - SHALLL populate this Patient resource's `.meta.source` element with the Data Source System's FHIR server URL
- SHALL omit patient references from the query statement(s) contained in the request's `query-string` parameter. *See [Search Conventions](request-queries.html)*

#### Step 3: Data Source System processes the request

When retrieving information using RESTful searches...
- the Data Source System processes the search according to the standard FHIR conventions, limiting response content to that pertaining to the specified patient. 

When responding to a Specialty Rx Query message...
- Before compiling the response, the Data Source System SHALL verify the patient match referenced in the request's `responder-patient` element.
  - If the match cannot be verified, the Data Source System SHALL return an OperationOutcome describing the error.

<br>

### Matching method Two: Deferred Patient Matching (Messaging Only)

In this approach, which applies only to the Specialty Rx Query message, the request contains only the Requesting System's Patient resource. 

#### Step 1: Populate the patient information in the Specialty Rx Query message

The Requesting System: 

- SHALL populate the `requester-patient` parameter with a reference to the **Requesting System's Patient resource** 
- SHALL omit patient references from the query statement(s) contained in the request's `query-string` parameter. *See [Search Conventions](request-queries.html)*

#### Step 2: Data Source processes the request message

The Data Source System performs patient matching using the request's patient identifying information before compiling the response. The system...

- SHALL locate a match to the responder patient referenced in the request's `requester-patient` parameter.
  - If the Data Source System cannot determine a single, confident match, it SHALL return an OperationOutcome describing the error.
- SHALL append a patient parameter containing the responder's patient ID to each search string supplied in a `query-string` parameter in the request.
  - For example, change the submitted query-string `"Condition"` to `"Condition?patient=[EHRPatient123]"`.

<br/>

### Additional Patient Processing Steps for Specialty Rx Messages
#### Populating patient information in response messages (Solicited and Unsolicited)

In the Specialty Rx Query Response and Query Response - Unsolicited messages, the Data Source System...

- *In both message types,* SHALL populate the `responder-patient` element with a reference to the **responder's Patient resource**
- *In the Specialty Rx Query message,* SHALL echo the **requester's Patient resource** in the `requester-patient` parameter and SHALL populate this Patient resource's `.meta.source` element with the Requesting System's FHIR server URL

The Data Source System then populates the results as below...

- Results for each search are populated in a searchset Bundle referenced by a `search-result` parameter.
- *In the Solicited model,* if a search is not successful, an OperationOutcome SHALL be included in the searchset Bundle and...
  - SHALL contain an issue with severity ERROR if query failed
  - SHALL contain an issue with severity ERROR  if the query or search parameter is not supported
  - SHALL specify a reason for the error
  - MAY fail the whole message if a query fails

#### Processing received response messages (Solicited and Unsolicited)

When the Requesting System processes a Specialty Rx Query Response or Query Response - Unsolicited message, it...

- *In the Solicited model*
  - SHALL verify that the `requester-patient` parameter contains a reference to the Requesting System's patient and that its `.meta.source` = requester's FHIR server URL
  - SHOULD confirm that the `responder-patient` parameter matches the Requesting System's patient
- *In the Unsolicited model* 
  - SHALL match the Patient referenced by the `responder-patient` parameter
  - SHOULD match the MedicationRequest in the `prescription` parameter (including referenced prescribing Practitioner and pharmacy Organization) to the related prescription. The receiving party can handle non-match situations according to their own rules, e.g., accept the message and add the patient to their system after a manual review

<br>