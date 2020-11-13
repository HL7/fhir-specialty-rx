### Systematic Query Workflows

Much of the information needed to fulfill a specialty medication can be retrieved systematically from the prescriber's EHR: allergies, conditions, active medications, etc. This section details those exchange flows:

- Solicited flow using the [Specialty Rx Query Response - Unsolicited message](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) only
- Solicited flow using RESTful searches through (a) a direct connection between the requesting system and the data source and (b) an intermediary
- Unsolicited flow using the [Specialty Rx Query request](StructureDefinition-specialty-rx-bundle-query.html) and [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) messages only
- Unsolicited flow using RESTful searches facilitated by an intermediary.

<br>

### Example Use Scenarios

#### "Solicited" workflow requesting patient information related to a prescription

In this scenario, a Requesting System receives a specialty medication prescription and then requests related patient information needed to fulfill it. 

The Requesting system either submits RESTful FHIR searches against the Data Source system, or transmits a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html) to the Data Source (or an Intermediary) containing searches for the desired information.

The Data Source System responds to the RESTful FHIR searches (in the first case) or returns a [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) containing the requested information (in the second).

#### "Unsolicited" workflow containing a predefined set of request information

In this scenario, a Data Source System shares patient information related to a specialty medication prescription that it has sent to the Requesting System. The Data Source System or its agent collects patient information associated with the prescription and transmits it in a [Specialty Rx Query Response - Unsolicited message](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html).

### Workflow Overview - Solicited and Unsolicited

In all workflow scenarios, Specialty Rx exchanges takes place after the specialty medication prescription has been received by the Requesting System (or received by a user of the system, for example by fax).

#### "Solicited" Workflow

1. The Requesting System initiates RESTful searches or a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html) when additional information is needed to facilitate fulfillment of a specialty medication prescription.

   - This might be triggered automatically by the Requesting System upon receiving an electronic prescription (NewRx) or 
   - A person using the Requesting System might initiate the process manually, for example after receiving a faxed prescription.
2. The Data Source System collects the requested information and responds to the RESTful searches or, if sent a Specialty Rx Query, responds with a [Specialty Rx Query Response message](StructureDefinition-specialty-rx-bundle-query-response.html).
   - Alternatively, if the Specialty Rx Query was sent to an intermediary, it retrieves the requested information using RESTful interactions with the data source and returns the results to the Requesting System in a Specialty Rx Query Response message.
3. (optional) Staff or the Requesting System itself initiates retrieval of information requiring human intervention, by requesting that the EHR prompt a clinic user to launch a SMART application *(see [Information Flows Requiring Human Interaction](human-interaction.html))*.
4. The Data Source System enables users to respond to those questions *(see [Information Flows Requiring Human Interaction](human-interaction.html))*.

  *Notes:*

- The response to a Specialty Rx Query is expected to typically be synchronous, but may be asynchronous, as determined with each request by the Data Source.
- The process may repeat one or more times, for example if the user of the Requesting System realizes they need additional information as a follow-up to information received in a previous response.
- The solicited workflow may occur after an unsolicited workflow.
  For example, the Data Source System transmits a new specialty medication prescription to a pharmacy and also initiates an "unsolicited" Specialty Rx Query Response to the pharmacy, containing related information. Upon review of the prescription and accompanying information, pharmacy staff realizes they need additional information and initiates a Specialty Rx Query message back to the Data Source System. 

#### "Unsolicited" Messaging Workflow

1. At the time that a specialty medication prescription is ordered, the Data Source System...

   - transmits the prescription to the pharmacy and/or other Requesting System
   - also collects related information and initiates a [Specialty Rx Query Response - Unsolicited message](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html)  to the Requesting System, to accompany the prescription

Alternatively, an intermediary notes the transmission of the prescription, retrieves associated patient information using RESTful interactions with the data source, and transmits it in a Specialty Rx Query Response - Unsolicited to the pharmacy and/or other Requesting System.

<br>

### Solicited - Messaging Only

In this flow, patient information is exchanged based on a request from a pharmacy or other party. The request is transmitted in a FHIR message to the data source who collects the requested information, collects it into are response FHIR message and returns it to the requester.

<div><p>
  <img src="high-level-exchange-flow-solicited.png" style="float:none">  
    </p>
</div>
<br>

### Solicited - RESTful Data Source

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

### Unsolicited - Messaging Only

In this flow, the prescribing system proactively sends a FHIR message containing patient information related to a prescription.

<div><p>
  <img src="high-level-exchange-flow-unsolicited.png" style="float:none">  
    </p>
</div>
<br>

### Unsolicited - RESTful Data Source

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

### Response Synchronicity

All messaging flows may be synchronous or asynchronous, to support situations where...

- the entire response content can be generated systematically (e.g., if the responding system contains all of the requested information) 
- systematic retrieval is possible, but the request must be queued or otherwise cannot be immediately processed
- a person must create some or all of the response content (e.g., by answering open-ended questions submitted in the request).

<br>

