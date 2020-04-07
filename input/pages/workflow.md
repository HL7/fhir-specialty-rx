###  System Roles

#### Requesting system

In the Specialty Medication Prescribing (Specialty Rx) workflow, the requesting system is used by a stakeholder that requires information to perform an activity related to a specialty medication prescription. 

The actors below may initiate a specialty Rx data request. They are referred to generally as *Third Party System* in the workflow scenarios below.

***Pharmacy***

   The pharmacy typically will:

- Receive the NewRx transaction requiring more information to be provided before it can be dispensed
- Request additional information from prescriber or their EHR system
- Determine when additional information necessary to dispense medication has been satisfied

***Other Third Parties*** (examples include but are not limited to intermediary, hub, manufacturer)

   These other parties typically will:

- Request additional information from prescriber or their EHR system
- Determine when additional information necessary to dispense medication has been satisfied

#### Responding system

The responding system in the Specialty Rx workflow is the electronic health record (EHR) system used by the prescriber of the specialty medication or associated staff. It is referred to as the *Prescriber System* in the workflow scenarios below.

The actors below respond to a specialty Rx data request:

***Prescriber***

   The prescriber typically will:

- Create a New Prescription using the NCPDP SCRIPT (NewRx) transaction requiring more information to be provided before it can be dispensed
- Provide appropriate responses to requests for information from other parties

***Prescriber Agent***

   The prescriber agent can:

- Provide appropriate responses to requests on behalf of the provider

***EHR System***

   The EHR system typically will:

- Respond automatically when a request from a third party is received
- Allow users to respond to requests for additional information when requested from other parties

### Exchange Workflows

#### "Solicited" Workflow

1. The Third Party System initiates a Specialty Rx Data Request when additional information relating to a specialty prescription is needed to facilitate dispensing or other activity.

- This might be triggered automatically by the Third Party System upon receiving an electronic prescription (NewRx) or 

- A person using the Third Party System might initiate the request manually, e.g., after receiving a faxed prescription

2. The Prescriber System collects the requested information and responds with a Specialty Rx Data Response.

  *Notes:*

- The response is typically asynchronous.
- The process may repeat one or more times, for example if the user of the Third Party System realizes they need additional information as a follow-up to information received in a previous Specialty Rx Data Response.
- The solicited workflow may follow an unsolicited workflow (described below).
  For example, the Prescriber system transmits a new specialty medication prescription to a pharmacy and also initiates an "unsolicited" Specialty Rx Data Response to the pharmacy, containing related information. Upon review of the prescription and accompanying information, pharmacy staff realizes they need additional information and initiates a Specialty Rx Data Request back to the Prescriber System. 

#### "Unsolicited" Workflow

1. At the time that a specialty medication prescription is ordered, the Prescriber System...

- transmits the prescription to the pharmacy and/or other Third Party System
- also collects related information and initiates a Specialty Rx Data Response to the Third Party System, to accompany the prescription

In both workflows, Specialty Rx Data exchanges takes place after the specialty medication prescription has been received by the Third Party System (or received by a user of the system, e.g., by fax).

### Example use scenarios

#### "Unsolicited" workflow containing a predefined set of request information

In this scenario, a Prescriber System sends information related to a specialty medication prescription previously sent to the Third Party System, (One-way exchange initiated by a Prescriber System)

The Prescriber System collects predefined information associated with a specialty medication prescription and initiates a Specialty Rx Data Response containing the information to a Third Party System.

The Specialty Rx Data Response bundle contains the following resources:

- MessageHeader
- MedicationRequest (reflecting the specialty medication prescription)
- Patient (the subject of the MedicationRequest)
- Practitioner (the prescriber of the MedicationRequest)
- Organization (the dispensing pharmacy)
- QuestionnaireResponse

​    *Related information, such as...*

- List (referencing requested allergies, conditions, etc.)
- AllergyIntolerance
- MedicationStatement
- Condition
- Observation
- Coverage



#### "Solicited" workflow referencing a predefined set of request information

In this scenario, a Third Party System requests information related to a specialty medication prescription it's received, The request refers to a predefined Questionnaire.

The Third Party system creates a Specialty Rx Data Request message bundle and submits it to the Prescriber System. The request bundle contains the following resources:

- MessageHeader
- MedicationRequest (reflecting the specialty medication prescription)
- Patient (the subject of the MedicationRequest)
- Practitioner (the prescriber of the MedicationRequest)
- Organization (the dispensing pharmacy)
- reference identifying a predefined Questionnaire. (The Prescriber System already has access to the predefined Questionnaire identified in the request.)

The Prescriber System collects the information specified in the predefined questionnaire and initiates an asynchronous Specialty Rx Data Response to the requesting Third Party System.

- *The response bundle contains resources as described above*



#### "Solicited" workflow requesting an ad-hoc set of information

In this scenario, a Third Party System requests an ad-hoc set of information related to a specialty medication prescription it's received. 

The Third Party system creates a Specialty Rx Data Request message bundle and submits it to the Prescriber System. The request bundle contains the same resources as identified in the previous example, except with the addition of a Questionnaire resource containing ad-hoc information requests.

The Prescriber System collects the information specified in the request's Questionnaire resource and initiates an asynchronous Specialty Rx Data Response to the requesting Third Party System.

- The response bundle contains the resources necessary to supply the requested information.

