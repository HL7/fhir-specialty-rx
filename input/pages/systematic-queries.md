Much of the information needed to fulfill a specialty medication can be retrieved systematically from the prescriber's EHR: allergies, conditions, active medications, and other patient information. This section details those exchange flows.

In all workflow scenarios, Specialty Rx exchanges takes place after the specialty medication prescription has been received by the pharmacy or other party involved in fulfilling the prescription. In the US, electronic prescriptions are typically transmitted using the NCPDP SCRIPT standard, though there are also occasions where prescriptions are received via fax or through other non-electronic methods.

This section...

- describes the two basic workflows defined in this guide for providing the pharmacy or other party  with patient information associated with a prescription: Solicited and Unsolicited 
- outlines RESTful and messaging-based approaches for satisfying those two basic workflows
- discusses synchronous versus asynchronous response expectations.

**Note that this guide does not require a given implementer to support both RESTful and messaging approaches.** Instead, each may implement one or both depending on their needs and the needs of their partners. Detailed implementation profiles are described in the [Capability Statements](capability-statements.html) section of the guide.

In addition, an intermediary may facilitate exchange between RESTful and messaging-based participants, which is described further in the [Intermediary Facilitation](intermediary.html) section of the guide.

<p></p>

### Solicited Workflow Overview

The "Solicited Workflow" is one in which a pharmacy or other Data Consumer system "solicits" patient information related to a specialty medication from a Data Source such as an EHR. Below is the sequence of events:

1. The pharmacy or other party (the Data Consumer in this workflow) receives a specialty medication prescription
2. If additional information is needed to fulfill the prescription, the Data Consumer system requests the information from the Data Source
3. The Data Source system returns the requested information
4. (optional) Staff involved in fulfilling the prescription (or the Data Consumer system itself) initiates retrieval of additional information requiring human intervention at the Data Source. 
   - The IG provides a method by which the Data Consumer system can ask the EHR to prompt a clinic user to provide additional information by launching a SMART application *(see [Information Flows Requiring Human Interaction](human-interaction.html))*.

This process may repeat one or more times, for example if the user of the Data Consumer system realizes they need additional information as a follow-up to information received in a previous response. Further, the solicited workflow may occur after an unsolicited workflow (described below).

<p></p>

### Unsolicited Workflow Overview

In the "Unsolicited Workflow", a Data Source system proactively transmits patient information to a pharmacy or other party involved in fulfilling a specialty medication prescription. 

1. The Data Source system transmits a specialty medication prescription to the pharmacy and/or other party involved in its fulfillment (the Data Consumer). (In the US, this transmission typically uses the NCPDP SCRIPT standard)
2. The Data Source collects related patient information and transmits it separately from the prescription to the Data Consumer system, to support fulfillment of the prescription
3. Alternatively, an intermediary notes the transmission of the prescription that occurred in Step 1, retrieves associated patient information using RESTful interactions with the Data Source, and transmits it to the pharmacy or other party

<p></p>

### Exchange Flows

#### Solicited - RESTful Data Source

In this flow, patient information is exchanged based on a request from a pharmacy or other party to a Data Source which responds to RESTful requests. 

The Data Consumer system employs standard FHIR RESTful searches to retrieve patient information from the Data Source. In this model, the Data Consumer must be able to locate and connect directly with the Data Source, for example when the two are part of the same umbrella organization.

In this model, the Data Consumer system is responsible for...

- determining the Data Source holding information about the patient for whom the prescription of interest was written

- locating the system endpoint information needed to connect with that Data Source

- performing RESTful searches directly against the Data Source.

<div><p>
  <img src="high-level-exchange-flow-solicited-rest.png" style="float:none">  
    </p>
</div>

<p></p>

#### Solicited - Messaging

In this flow, patient information is exchanged based on a request from a pharmacy or other party. The request is transmitted in a [Specialty Rx Query request](StructureDefinition-specialty-rx-bundle-query.html) message to the Data Source who collects the requested information, collects it into a [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) message and returns it to the Data Consumer.

<div><p>
  <img src="high-level-exchange-flow-solicited.png" style="float:none">  
    </p>
</div>

<p></p>

#### Unsolicited - RESTful Data Source

This guide defines an unsolicited data "push" model that uses FHIR messaging (below). This approach aligns with the current environment in which it is expected that all prescribing systems are able to exchange with all pharmacies in the US, the bulk of prescriptions are transmitted through exchange networks, and direct connections between EHRs and pharmacies are uncommon.

However, the Data Source may leverage an intermediary to enable patient information to be collected and sent to a pharmacy or other party in FHIR message form, with the Data Source interacting solely through standard RESTful requests. The [Intermediary Facilitation](intermediary.html) section describes this approach. 

<p></p>

#### Unsolicited - Messaging

In this flow, the prescribing system proactively sends a   [Specialty Rx Query Response - Unsolicited message](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) containing patient information related to a prescription.

<div><p>
  <img src="high-level-exchange-flow-unsolicited.png" style="float:none">  
    </p>
</div>

<p></p>

### Messaging Synchronicity

All messaging flows may be synchronous or asynchronous, as defined in the [$process-message operation](https://www.hl7.org/fhir/messageheader-operation-process-message.html).

<br>

