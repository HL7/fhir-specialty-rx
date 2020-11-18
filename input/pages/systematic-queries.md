Much of the information needed to fulfill a specialty medication can be retrieved systematically from the prescriber's EHR: allergies, conditions, active medications, and other patient information. This section details those exchange flows.

In all workflow scenarios, Specialty Rx exchanges takes place after the specialty medication prescription has been received by the pharmacy or other party involved in fulfilling the prescription. In the US, electronic prescriptions are typically transmitted using the NCPDP SCRIPT standard, though there are also occasions where prescriptions are received via fax or through other non-electronic methods.

This section...

- describes the two basic workflows defined in this guide for providing the pharmacy or other party  with patient information associated with a prescription: Solicited and Unsolicited 
- outlines RESTful and messaging-based approaches for satisfying those two basic workflows
- discusses synchronous versus asynchronous response expectations.

**Note that this guide does not require a given implementer to support both RESTful and messaging approaches.** Instead, each may implement one or both depending on their needs and the needs of their partners. Detailed implementation profiles are described in the Capability Statement section of the guide.

In addition, an intermediary may facilitate exchange between RESTful and messaging-based participants, which is described further in the [Intermediary Facilitation](intermediary.html) section of the guide.

<br>

### Solicited Workflow Overview

The "Solicited Workflow" is one in which a pharmacy or other Requesting system "solicits" patient information related to a specialty medication from a Data Source such as an EHR. Below is the sequence of events:

1. The pharmacy or other party receives a specialty medication prescription
2. If additional information is needed to fulfill the prescription, the Requesting System requests the information from the Data Source
3. The Data Source System returns the requested information
4. (optional) Staff at the requesting party (or the Requesting System itself) initiates retrieval of additional information requiring human intervention at the Data Source. 
   - The IG provides a method by which the Requesting System can ask the EHR to prompt a clinic user to provide additional information by launching a SMART application *(see [Information Flows Requiring Human Interaction](human-interaction.html))*.

  *Notes:*

- The process may repeat one or more times, for example if the user of the Requesting System realizes they need additional information as a follow-up to information received in a previous response.
- The solicited workflow may occur after an unsolicited workflow. For example, the Data Source System transmits a new specialty medication prescription to a pharmacy and also initiates an "unsolicited" Specialty Rx Query Response to the pharmacy, containing related information. Upon review of the prescription and accompanying information, pharmacy staff realizes they need additional information and initiates a Specialty Rx Query message back to the Data Source System. 

<br>

### Unsolicited Workflow Overview

In the "Unsolicited Workflow", a Data Source system proactively transmits patient information to a pharmacy or other party involved in fulfilling a specialty medication prescription. 

1. The Data Source System transmits a specialty medication prescription to the pharmacy and/or other Requesting System. (In the US, this transmission typically uses the NCPDP SCRIPT standard)
2. The Data Source collects related patient information and transmits it separately from the prescription to the Requesting System, to support fulfillment of the prescription
3. Alternatively, an intermediary notes the transmission of the prescription that occurred in Step 1, retrieves associated patient information using RESTful interactions with the data source, and transmits it to the pharmacy or other party

<br>

### Exchange Flows

#### 1. Solicited - RESTful Data Source

In this flow, patient information is exchanged based on a request from a pharmacy or other party to a data source responds to RESTful requests. 

The Requesting System employs standard FHIR RESTful searches to retrieve patient information from the Data Source. In this model, the requester must be able to locate and connect directly with the data source, for example when the two are part of the same umbrella organization.

In this model, the requesting system is responsible for...

- determining the data source holding information about the patient for whom the the prescription of interest was written

- locating the system endpoint information needed to connect with that data source

- performing RESTful searches directly against the data source.

  <br>

<div><p>
  <img src="high-level-exchange-flow-solicited-rest.png" style="float:none">  
    </p>
</div>
<br>

#### 2. Solicited - Messaging

In this flow, patient information is exchanged based on a request from a pharmacy or other party. The request is transmitted in a [Specialty Rx Query request](StructureDefinition-specialty-rx-bundle-query.html) message to the data source who collects the requested information, collects it into a [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) message and returns it to the requester.

<br>

<div><p>
  <img src="high-level-exchange-flow-solicited.png" style="float:none">  
    </p>
</div>

<br>

#### 3.Unsolicited - RESTful Data Source

This guide defines an unsolicited data "push" model that uses FHIR messaging (below). This approach aligns with the current environment in which it is expected that all prescribing systems are able to exchange with all pharmacies in the US, the bulk of prescriptions are transmitted through exchange networks, and direct connections between EHRs and pharmacies are uncommon.

However, the data source may leverage an intermediary to enable patient information to be collected and sent to a pharmacy or other party in FHIR message form, with the data source interacting solely through standard RESTful requests. The [Intermediary Facilitation](intermediary.html) section describes this approach. 

<br>

#### 4. Unsolicited - Messaging

In this flow, the prescribing system proactively sends a   [Specialty Rx Query Response - Unsolicited message](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) containing patient information related to a prescription.

<div><p>
  <img src="high-level-exchange-flow-unsolicited.png" style="float:none">  
    </p>
</div>
<br>

### Messaging Synchronicity

All messaging flows may be synchronous or asynchronous, to support situations where...

- the Data Source system can always respond synchronously 
- the Data Source typically responds synchronously, but a given request cannot be immediately processed
- the Data source always returns results asynchronously.

**Note:** The `async` and `response-url` Process Message parameters are not to be used when exchanging Specialty Rx messages.

<br>

