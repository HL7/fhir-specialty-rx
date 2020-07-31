### Message Flows and System Roles

#### Solicited

In this flow, patient information is exchanged based on a request from a pharmacy or other party.

<div><p>
  <img src="high-level-exchange-flow-solicited.png" style="float:none">  
    </p>
</div>
<br>

#### Unsolicited

In this flow, the prescribing system proactively sends patient information related to a prescription.

<div><p>
  <img src="high-level-exchange-flow-unsolicited.png" style="float:none">  
    </p>
</div>

<br>

###  System Roles

#### Requesting system

In the Specialty Rx workflow, the requesting system is used by a stakeholder that requires information to perform an activity related to a specialty medication prescription. 

The actors below may initiate a Specialty Rx request message. They are referred to generally as *Third Party System* in the workflow scenarios below.

***Pharmacy***

   The pharmacy system typically will:

- Receive the NewRx transaction requiring more information to be provided before it can be dispensed
- Enable staff to request additional information from the prescriber or their electronic health record (EHR) system using Specialty Rx Query or Specialty Rx Questionnaire messages

***Other Third Party Systems*** (examples include but are not limited to systems used by a specialty hub or manufacturer)

   These systems typically will:

- Enable staff to request information related to a prescription from the prescriber or their electronic health record (EHR) system using Specialty Rx Query or Specialty Rx Questionnaire messages

#### Responding system

The responding system in the Specialty Rx workflow is the EHR system used by the prescriber of the specialty medication or associated staff. It is referred to as the *Prescriber System* in the workflow scenarios below.

The actors below may participate in generation of a response to a Specialty Rx request:

***Prescriber***

   The prescriber typically will:

- Provide appropriate responses to Specialty Rx Questionnaire requests submitted by other parties

***Prescriber Agent***

   The prescriber agent can:

- Provide appropriate responses to submitted Specialty Rx Questionnaire requests, on behalf of the prescriber

***EHR System***

   The EHR system typically will:

- Respond automatically when a Specialty Rx Query message is received, returning a Specialty Rx Query Response based on data stored in the patient's electronic chart
- Enable users to respond to Specialty Rx Questionnaire messages containing requests for additional information

### Exchange Workflows

#### "Solicited" Workflow

1. The Third Party System initiates a Specialty Rx Query when additional information relating to a specialty prescription is needed to facilitate dispensing or other activity.

   - This might be triggered automatically by the Third Party System upon receiving an electronic prescription (NewRx) or 
   - A person using the Third Party System might initiate the request manually, e.g., after receiving a faxed prescription
2. The Prescriber System collects the requested information and responds with a Specialty Rx Query Response.
3. (optional) Staff or the Third Party System itself initiates a Specialty Rx Questionnaire message when further information is needed.
4. The Prescriber System enables users to respond to questions in the Specialty Rx Questionnaire,  and returns a Specialty Rx Questionnaire Response.

  *Notes:*

- The response to a Specialty Rx Query is expected to typically be synchronous.
- The response to a Specialty Rx Questionnaire is expected to typically be asynchronous--in order to allow staff to answer questions and/or locate attachments.
- The process may repeat one or more times, for example if the user of the Third Party System realizes they need additional information as a follow-up to information received in a previous response.
- The solicited workflow may occur after an unsolicited workflow.
  For example, the Prescriber system transmits a new specialty medication prescription to a pharmacy and also initiates an "unsolicited" Specialty Rx Query Response to the pharmacy, containing related information. Upon review of the prescription and accompanying information, pharmacy staff realizes they need additional information and initiates a Specialty Rx Query or Specialty Rx Questionnaire messsage back to the Prescriber System. 

#### "Unsolicited" Workflow

1. At the time that a specialty medication prescription is ordered, the Prescriber System...

   - transmits the prescription to the pharmacy and/or other Third Party System
   - also collects related information and initiates a Specialty Rx Query Response - Unsolicited to the Third Party System, to accompany the prescription

In both workflows, Specialty Rx exchanges takes place after the specialty medication prescription has been received by the Third Party System (or received by a user of the system, e.g., by fax).

### Options for compiling a response

The flow may be synchronous or asynchronous, enabling it to support both...

- situations where the entire response content can be generated systematically (e.g., if the responding system contains all of the requested information) 

- situations where a person must create some or all of the response content (e.g., by answering open-ended questions submitted in the request)

### Example use scenarios

#### "Unsolicited" workflow containing a predefined set of request information

In this scenario, a Prescriber System sends information related to a specialty medication prescription previously sent to the Third Party System. The Prescriber System collects patient information associated with the prescription and initiates a Specialty Rx Query Response - Unsolicited message containing that information.

#### "Solicited" workflow requesting an ad-hoc set of information

In this scenario, a Third Party System requests an ad-hoc set of information related to a specialty medication prescription it's received. 

The Third Party system creates a Specialty Rx Query message and submits it to the Prescriber System. The request bundle specifies searches for the desired information.

The Prescriber System collects the information specified in the request and returns a Specialty Rx Query Response to the requesting system. The response bundle contains the resources containing the requested information.

<br/>