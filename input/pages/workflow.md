### Exchange Flows and System Roles

#### Solicited - Messaging Only

In this flow, patient information is exchanged based on a request from a pharmacy or other party. The request is transmitted in a FHIR message to the data source who collects the requested information, collects it into are response FHIR message and returns it to the requester.

<div><p>
  <img src="high-level-exchange-flow-solicited.png" style="float:none">  
    </p>
</div>
<br>

#### Solicited - RESTful Data Source

In this flow, patient information is also exchanged based on a request from a pharmacy or other party. However, in this model the data source responds to RESTful requests rather than accepting a FHIR request message and returning a message response. 

There are two variations to this flow: **direct connect** and **intermediary-facilitated**.

**Direct Connect**

In this model, the requester must be able to locate and connect directly with the data source, for example when the two are part of the same umbrella organization.

In the direct connect model, the requesting system is responsible for...

- determining the data source holding information about the patient for whom the the prescription of interest was written
- locating the system endpoint information needed to connect with that data source
- performing RESTful searches directly against the data source.

**Intermediary-Facilitated**

This model accommodates requesters that are unable to locate and connect directly with the data source, while still enabling the data source to respond using standard RESTful interactions.

Pharmacies in the US typically receive prescriptions through network intermediaries. Because of this, their systems do not maintain direct connections to individual prescriber system instances, and they further lack the information needed to determine the correct data source endpoint related to a given prescription and patient. These pharmacies are unable to submit RESTful requests directly to the data source.

In this situation, an intermediary can facilitate RESTful data source interactions on behalf of the requesting party--using the routing information and connection it possesses. 

In this flow: 

- the requester submits a FHIR request message to the intermediary
- the intermediary locates the correct data source and connection specifics based on information in the request message
- the intermediary performs RESTful patient matching and data requests against the data source, and packages the results into a response FHIR message
- the intermediary returns the FHIR response message to the requester.

<br>

<div><p>
  <img src="high-level-exchange-flow-solicited-facilitated-rest.png" style="float:none"> 
    </p>
</div>

<br>

#### Unsolicited - Messaging Only

In this flow, the prescribing system proactively sends a FHIR message containing patient information related to a prescription.

<div><p>
  <img src="high-level-exchange-flow-unsolicited.png" style="float:none">  
    </p>
</div>
<br>

#### Unsolicited - RESTful Data Source

In this flow, an intermediary facilitates the sending of patient information in conjunction with a new specialty medication prescription.

This model enables patient information to be collected and sent to a pharmacy or other party in FHIR message form, with the data source interacting solely through standard RESTful requests.

An intermediary facilitates the process as follows: 

- the prescribing system transmits a prescription through the intermediary to the specialty pharmacy
- the intermediary uses information from the prescription to locate the data source's FHIR endpoint containing the subject patient's information
- the intermediary performs RESTful patient matching and data requests against the data source, and packages the results into a unsolicited FHIR message
- the intermediary transmits the FHIR message to the pharmacy or other party.

<br>

<div><p>
  <img src="high-level-exchange-flow-unsolicited-facilitated-rest.png" style="float:none"> 
    </p>
</div>

<br>

###  System Roles

#### Requesting System

In the Specialty Rx workflow, the requesting system is used by a stakeholder that requires information to perform an activity related to a specialty medication prescription. 

The actors below may initiate a Specialty Rx request message. They are referred to generally as *Third Party System* in the workflow scenarios below.

***Pharmacy***. The pharmacy system typically will:

- Receive the NewRx transaction requiring more information to be provided before it can be dispensed
- Enable staff to request additional information from the prescriber or their electronic health record (EHR) system (using a Specialty Rx Query message, Specialty Rx Questionnaire message, or RESTful interaction)

***Other Third Party Systems*** (examples include but are not limited to systems used by a specialty hub or manufacturer). These systems typically will:

- Enable staff to request information related to a prescription from the prescriber or their electronic health record (EHR) system (using a Specialty Rx Query message, Specialty Rx Questionnaire message, or RESTful interaction)

#### Data Source System

The responding system in the Specialty Rx workflow is the EHR system used by the prescriber of the specialty medication or associated staff. It is referred to as the *Data Source System* in the workflow scenarios below.

The Data Source system typically will...

- Respond to queries submitted by the dispensing pharmacy or other party.
  - ***If supporting Specialty Rx messaging:*** Respond systematically when a Specialty Rx Query message is received, returning a Specialty Rx Query Response based on data stored in the patient's electronic chart
  - ***If supporting RESTful data source interactions:*** Respond to RESTful patient matching and search requests based on data stored in the patient's electronic chart
- Enable users to respond to Specialty Rx Questionnaire messages containing requests for additional information

<br>

#### Intermediary System

An Intermediary System facilitates the exchange of information between other parties. 

- In the messaging-based exchanges, an intermediary may use its knowledge of network participants and connection information to route prescriptions and other data exchanges between sources and receiving parties.
- In the intermediary-facilitated RESTful exchanges described above, the intermediary performs additional actions to enable data sources that only support RESTful interactions to interact with messaging-based partners.

<br>

#### Prescriber

   The prescriber typically will:

- Provide appropriate responses to Specialty Rx Questionnaire requests submitted by other parties

#### Prescriber Agent

   The prescriber agent can:

- Provide appropriate responses to submitted Specialty Rx Questionnaire requests, on behalf of the prescriber

<br>

### High-Level Workflows

In all workflow scenarios, Specialty Rx exchanges takes place after the specialty medication prescription has been received by the Third Party System (or received by a user of the system, for example by fax).

#### "Solicited" Workflow

1. The Third Party System initiates a Specialty Rx Query when additional information relating to a specialty prescription is needed to facilitate dispensing or other activity.

   - This might be triggered automatically by the Third Party System upon receiving an electronic prescription (NewRx) or 
   - A person using the Third Party System might initiate the request manually, for example after receiving a faxed prescription
2. The Data Source System collects the requested information and responds with a Specialty Rx Query Response.
   - Alternatively, an intermediary retrieves the requested information using RESTful interactions with the data source.
3. (optional) Staff or the Third Party System itself initiates a Specialty Rx Questionnaire message when further information is needed.
4. The Data Source System enables users to respond to questions in the Specialty Rx Questionnaire,  and returns a Specialty Rx Questionnaire Response.

  *Notes:*

- The response to a Specialty Rx Query is expected to typically be synchronous.
- The response to a Specialty Rx Questionnaire is expected to typically be asynchronous--in order to allow staff to answer questions and/or locate attachments.
- The process may repeat one or more times, for example if the user of the Third Party System realizes they need additional information as a follow-up to information received in a previous response.
- The solicited workflow may occur after an unsolicited workflow.
  For example, the Data Source System transmits a new specialty medication prescription to a pharmacy and also initiates an "unsolicited" Specialty Rx Query Response to the pharmacy, containing related information. Upon review of the prescription and accompanying information, pharmacy staff realizes they need additional information and initiates a Specialty Rx Query or Specialty Rx Questionnaire message back to the Data Source System. 

#### "Unsolicited" Messaging Workflow

1. At the time that a specialty medication prescription is ordered, the Data Source System...

   - transmits the prescription to the pharmacy and/or other Third Party System
   - also collects related information and initiates a Specialty Rx Query Response - Unsolicited to the Third Party System, to accompany the prescription

Alternatively, an intermediary notes the transmission of the prescription, retrieves associated patient information using RESTful interactions with the data source, and transmits it in a Specialty Rx Query Response - Unsolicited to the pharmacy and/or other Third Party System.

<br>

### Response Synchronicity

The flow may be synchronous or asynchronous, enabling it to support both...

- situations where the entire response content can be generated systematically (e.g., if the responding system contains all of the requested information) 

- situations where a person must create some or all of the response content (e.g., by answering open-ended questions submitted in the request)

<br>

### Example Use Scenarios

#### "Unsolicited" workflow containing a predefined set of request information

In this scenario, a Data Source System sends information related to a specialty medication prescription previously sent to the Third Party System. The Data Source System collects patient information associated with the prescription and initiates a Specialty Rx Query Response - Unsolicited message containing that information.

#### "Solicited" workflow requesting an ad-hoc set of information

In this scenario, a Third Party System requests an ad-hoc set of information related to a specialty medication prescription it's received. 

The Third Party system creates a Specialty Rx Query message and submits it to the Data Source System. The request bundle specifies searches for the desired information.

The Data Source System collects the information specified in the request and returns a Specialty Rx Query Response to the requesting system. The response bundle contains the resources containing the requested information.

<br/>