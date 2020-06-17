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

- **Pre-Match the Patient** and refer to the patient using the responder's identifier. This is typically accomplished by referencing the responder's Patient resource ID in the request

  or

- **Defer Patient Matching** and refer to the patient using the requester's own Patient resource. In this method, patient matching is performed by the responder as a pre-step to creating the Communication response.

<br>

#### Method One: Patient Pre-Match

Depending on the scenario, the requesting system may obtain the responder's Patient resource in one of two ways:

- receive it in a previous Communication from the responder system
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

##### Step 2: Populate the patient information in the CommunicationRequest 

After obtaining the responder's Patient resource, the requester: 

- MUST populate the .subject element with a reference to the **requester's Patient resource** 
- MUST populate the .about element with the **responder's Patient resource**, to enable the responder to confirm the query's patient identifying parameter before responding
  - MUST populate this patient resource's .meta.source element with the responder system's FHIR server URL
- MUST refer to the patient in the query statement(s) contained in the CommunicationRequest's payload element using the **responder's Patient resource ID** that corresponds to the Patient resource in the .about element.

##### Step 3: Responder processes the CommunicationRequest

The responding system uses the CommunicationRequest's patient identifying information as follows. 

Before compiling the response, the system...

- MUST verify the responder patient match referenced in the CommunicationRequest.about element
- MUST verify that the .payload element's query string references the patient resource ID present in the .about element
- MUST fail the query if the .payload element's query string contains a searchParameter that is not recognized/supported.

<br>

#### Method Two: Deferred Patient Matching

In this approach, the CommunicationRequest does contains only the requester's Patient resource. Matching to the responder's patient is performed as a pre-step to creating the Communication response.

##### Step 1: Populate the patient information in the CommunicationRequest 

The requester: 

- MUST populate the .subject element with a reference to the **requester's Patient resource** 
- MUST omit patient references from the query statement(s) contained in the CommunicationRequest's payload element. For example, a query for the patient's conditions is expressed simply as... 
  - "valueString" : "Condition"

<br>

------

*[For discussion... is this an option?... Referencing a logical patient identifier in the request*

- If the responder's logical patient identifier is available (such as a Medical Record Number / MRN), that identifier may be used in the query string as follows: [Resource]?patient.identifier={[system]}|[code]

  For example:

  "valueString" : "Condition?patient.identifier=http://uhealth.org/mrn|1032702"

<br>

##### Step 3: Responder processes the CommunicationRequest

The responding system performs patient matching using the CommunicationRequest's patient identifying information as follows. 

Before compiling the response, the system...

- MUST locate a match to the responder patient referenced in the CommunicationRequest.subject element
- MUST append a patient parameter containing the responder's patient ID to each query string in the CommunicationRequest.payload element 
  - Example: Change *"Condition"* in the request to *"Condition?patient=[responder's Patient ID]"*
- MUST fail the query if the .payload element's query string contains a searchParameter that is not recognized/supported.

<br>

### Building the Communication response (Solicited and Unsolicited)

In the Communication resource, the responder identifies the patient as follows...

- *In both models,* MUST populate the Communication.subject element with a reference to the **responder's Patient resource**
- *In the Solicited model,* MUST echo the **requester's Patient resource** (submitted in the CommunicationRequest.subject) in Communication.about. And MUST populate this patient resource's .meta.source element with the requester's FHIR server URL

The responder then populates the results as below...

- content MUST be reference to a List (unless an error)
  - If no results the list MUST have emptyReason
- content for the following payloads SHOULD be included:
  - Condition?patient=[patient]
  - AllergyIntolerance?patient=[patient]
  - Observation?patient=[patient]&category=vital-signs&date=”date period range”	
  - Coverage?patient=[patient]
  - MedicationStatement?patient=[patient]
- *In the Solicited model,* content MUST be a reference to OperationOutcome if query is non-success
  - MUST have issue with severity ERROR if query failed
  - MUST have issue with severity ERROR  if query or searchParameter not supported
  - Must specify a reason for the error
  - MAY fail the whole message if a query fails

<br>

### Processing the received Communication (Solicited and Unsolicited)

When the requester processes the Communication response, it...

- *In the Solicited model*
  - MUST verify that the Communication.about element contains a reference to the requester's patient ( .meta.source = requester's FHIR server URL )
  - SHOULD confirm that the responder's Patient in the Communication.subject element matches the pharmacy's patient echoed back in Communication.about
- *In the Unsolicited model* 
  - MUST match the responder's Patient in the Communication.subject element
  - SHOULD match the MedicationRequest in Communication.about to the related prescription
    - The receiving party can handle no-match according to their own rules, e.g., accept the message and add the patient to their system after a manual review
- *In both models*
  - MUST support content string, attachment and reference
  - MUST support content reference that contains either List and OperationOutcome resource.

<br>

<br>