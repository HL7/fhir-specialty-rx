The Specialty Rx process supports two exchange patterns: 

- Solicited Model: A pharmacy or other party requests patient information from an EHR or other data source
- Unsolicited Model: A data source pushes patient data to a recipient proactively--without having received a request

Relating to both of those models, the sections below describe the requester's and data source's steps and responsibilities for: 

- identifying / matching the patient   *(solicited model)*
- specifying the desired data   *(solicited model)*
- producing the data   *(solicited and unsolicited models)*
- consuming the data   *(solicited and unsolicited models)*

<br>

### Matching the patient and specifying the request (Solicited Model)

In the *solicited model*, where a pharmacy or other party requests patient information from an EHR or other responder, the requester may either...

- **Defer Patient Matching** and refer to the patient using the requester's own Patient resource. In this method, patient matching is performed by the responder as a pre-step to creating its response.

  or

- **Pre-Match the Patient** and refer to the patient using the responder's identifier. This is typically accomplished by referencing the responder's Patient resource ID in the request

#### Matching method One: Deferred Patient Matching

In this approach, the request message contains only the requester's Patient resource. 

##### Step 1: Populate the patient information in the Specialty Rx Query 

The requester: 

- MUST populate the requester-patient parameter with a reference to the **requester's Patient resource** 
- MUST omit patient references from the query statement(s) contained in the request's query-string parameter. *See [Search Conventions](request-queries.html)*

##### Step 2: Responder processes the request

The responding system performs patient matching using the request's patient identifying information before compiling the response. The system...

- MUST locate a match to the responder patient referenced in the request's requester-patient parameter
- MUST append a patient parameter containing the responder's patient ID to each search string supplied in a request's query-string paramter 
  - For example, change the submitted query-string*"Condition"* to *"Condition?patient=[EHRPatient123]"*

<br/>

#### Matching Method Two: Patient Pre-Match

Depending on the scenario, the requesting system may obtain the responder's Patient resource in one of two ways:

- receive it in a previous FHIR exchange with the responder system
- request it using the Patient/$match operation (described below)

##### Step 1: Obtain the responder's Patient resource using Patient/$match

In this scenario, the requester submits a patient match operation against the responder's server: 

- URL: [base]/Patient$match

*Input parameters.*  In the Specialty Rx process, this request MUST contain two parameters:

- Patient resource representing the requester's patient record
- The *onlyCertainMatches* parameter with the value = true. This prevents the responder from returning multiple possible Patient matches.

*Output parameter.*  The $match operation returns a Bundle containing...

- the single Patient resource that the responder has confidently matched to the requester's patient

  or 

- an OperationOutcome resource if the responder is unable to return a patient, containing further advice regarding patient selection.

##### Step 2: Populate the patient information in the request

After obtaining the responder's Patient resource, the requester: 

- MUST populate the request's requester-patient parameter with a reference to the **requester's Patient resource** 
- MUST populate the responder-patient parameter with the **responder's Patient resource**
  - MUST populate this patient resource's .meta.source element with the responder system's FHIR server URL
- MUST omit patient references from the query statement(s) contained in the request's query-string parameter. *See [Search Conventions](request-queries.html)*

##### Step 3: Responder processes the request

Before compiling the response, the responding system MUST verify the patient match referenced in the request's responder-patient element.

<br>

### Building the response (Solicited and Unsolicited)

In the response, the responder identifies the patient as follows...

- *In both models,* MUST populate the responder-patient element with a reference to the **responder's Patient resource**
- *In the Solicited model,* MUST echo the **requester's Patient resource** in the requester-patient parameter and MUST populate this Patient resource's .meta.source element with the requester's FHIR server URL

The responder then populates the results as below...

- Results for each search are populated in a searchset Bundle referenced by a search-result parameter
- *In the Solicited model,* if a search is not successful, an OperationOutcome must be included in the searchset Bundle and...
  - MUST contain an issue with severity ERROR if query failed
  - MUST contain an issue with severity ERROR  if the query or search parameter is not supported
  - Must specify a reason for the error
  - MAY fail the whole message if a query fails

<br>

### Processing the received response (Solicited and Unsolicited)

When the requester processes the response, it...

- *In the Solicited model*
  - MUST verify that the requester-patient parameter contains a reference to the requester's patient and that its .meta.source = requester's FHIR server URL
  - SHOULD confirm that the responder-patient parameter matches the pharmacy's patient
- *In the Unsolicited model* 
  - MUST match the Patient referenced by the responder-patient parameter
  - SHOULD match the MedicationRequest in the prescription parameter (including referenced prescribing Practitioner and pharmacy Organization) to the related prescription
    - The receiving party can handle no-match according to their own rules, e.g., accept the message and add the patient to their system after a manual review

<br>