Pharmacies in the US typically receive prescriptions through network intermediaries. Because of this, their systems do not maintain direct connections to individual prescriber system instances, and they further lack the information needed to determine the correct Data Source endpoint related to a given prescription and patient. These pharmacies are unable to submit RESTful requests directly to the Data Source.

In this situation, an intermediary may facilitate RESTful Data Source interactions on behalf of the requesting party--using the routing information and connection it possesses. 

Likewise, an EHR that conforms with the Specialty Rx RESTful Data Source profile may leverage an intermediary so that it can fulfill query requests from messaging-based pharmacies and transmit "unsolicited" information related to prescriptions it sends to these pharmacies.

This section describes these exchanges. 

<p></p>

### Intermediary-Facilitated Solicited Workflow

This exchange model accommodates requesters that... 

- have implemented only the Specialty Rx messages, or
- are unable to locate and/or connect directly with the Data Source associated with the prescription

... while enabling the Data Source to respond using standard RESTful interactions.

In this flow: 

- the requester submits a FHIR request message to the intermediary
- the intermediary locates the correct Data Source and connection specifics based on information in the request message
- the intermediary performs RESTful patient matching and data requests against the Data Source, and packages the results into a response FHIR message
- the intermediary returns the FHIR response message to the requester.

<p></p>

<div><p>
  <img src="high-level-exchange-flow-solicited-facilitated-rest.png" style="float:none"> 
    </p>
</div>

<p></p>

### Intermediary-Facilitated Unsolicited Workflow

In this flow, an intermediary facilitates the sending of patient information in conjunction with a new specialty medication prescription--from a RESTful Data Source to a messaging-based recipient.

This model enables patient information to be collected and sent to a pharmacy or other party in FHIR message form, with the Data Source interacting solely through standard RESTful requests.

An intermediary facilitates the process as follows: 

- the prescribing system transmits a prescription through the intermediary to the specialty pharmacy
- the intermediary uses information from the prescription to locate the Data Source's FHIR endpoint containing the subject patient's information
- the intermediary performs RESTful patient matching and data requests against the Data Source, and packages the results into an unsolicited FHIR message
- the intermediary transmits the FHIR message to the pharmacy or other party.

<p></p>

<div><p>
  <img src="high-level-exchange-flow-unsolicited-facilitated-rest.png" style="float:none"> 
    </p>
</div>
<br>