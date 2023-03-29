### Use Cases

The exchanges described in this implementation guide all support the goal of supplying information to those involved in fulfilling a patient's specialty medication prescription. The guide supports three basic use cases:

* As a party fulfilling the prescription, I need to retrieve patient clinical or coverage information from their medical records. 
  * *[Solicited Flow](systematic-queries.html#solicited-workflow-overview) section of [Systematic Query Workflows](systematic-queries.html)*
  
* As a party fulfilling the prescription, I need to ask a question of the prescriber or their staff. 
  * *[Information Flows Requiring Human Interaction](human-interaction.html)*

* As a party fulfilling the prescription, I need to request patient consent or other authorizations.
  * *[Consent Workflows](consent-workflow.html)*

* As the prescriber of the prescription, I want to proactively supply clinical, coverage or consent information from the patient's medical records to a party fulfilling the prescription. 
  * *[Unsolicited Flow](systematic-queries.html#unsolicited-workflow-overview) section of [Systematic Query Workflows](systematic-queries.html)*

<p></p>

###  Human Roles

#### Staff Fulfilling a Prescription

Staff at the pharmacy, specialty Hub or other party involved in fulfilling the prescription. These people identify information needs that result in information exchanges, and use the provided information. These are users of a Data Consumer system.

#### Prescriber

The prescriber provides responses to information requests that require human interaction, such as clarifications to aspects of a prescription. The prescriber is a user of a Data Source system.

#### Prescriber Agent

The prescriber agent can provide responses on behalf of the prescriber. Example: clinic staff. A prescriber agent is a user of a Data Source system.

<p></p>

###  System Roles

#### Data Consumer System

In the Specialty Rx workflow, the Data Consumer system is one used by a stakeholder who participates in fulfilling specialty medication prescriptions. It may be a pharmacy system or a system used by another party such as a specialty Hub or pharmaceutical manufacturer.

A Data Consumer System...

- enables staff to request patient information from the prescriber's electronic health record (EHR) system using [RESTful searches](searches.html) or a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html)
- if supporting Specialty Rx messaging, receives [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) and [Specialty Rx Query Response - Unsolicited](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) messages
- enables staff to ask additional questions or request supporting information requiring human attention by prompting an EHR user to launch and interact with a SMART application, using a [Specialty Rx SMART Launch Task](StructureDefinition-specialty-rx-task-smart-launch.html)
- enables staff to request patient consent or other authorizations using a [Specialty Rx Consent Request Task](StructureDefinition-specialty-rx-task-consent-request.html).

#### Data Source System

The responding system in the Specialty Rx workflow is the EHR system used by the prescriber of the specialty medication or associated staff.

The Data Source system typically will...

- *(If supporting RESTful Data Source interactions):* Respond to RESTful patient matching and search requests based on data stored in the patient's electronic chart
- *(If supporting Specialty Rx messaging):* Respond systematically when a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html) is received, returning a [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) based on data stored in the patient's electronic chart. It may also send [Specialty Rx Query Response - Unsolicited](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) messages proactively when a prescription is written
- Enable staff to respond to additional questions or supporting information requests that require human attention by accepting a [Specialty Rx SMART Launch Task](StructureDefinition-specialty-rx-task-smart-launch.html) and then prompting an EHR user to launch and interact with the requesting party's SMART application.
- Enable staff to respond to a request for patient consent or other authorizations by accepting a [Specialty Rx Consent Request Task](StructureDefinition-specialty-rx-task-consent-request.html) and then enabling an EHR user to obtain authorization and update the task.

#### Intermediary System

An Intermediary system facilitates the exchange of information between other parties. This role is optional and assists with Data Consumer system and/or Data Source system responsibilities when desired. See [Intermediary Facilitation](intermediary.html).

- In the messaging-based exchanges, an intermediary may use its knowledge of network participants and connection information to route prescriptions and other data exchanges between sources and receiving parties.
- In the intermediary-facilitated RESTful exchanges described above, the intermediary performs additional actions to enable Data Sources that only support RESTful interactions to interact with messaging-based partners.

<br>

