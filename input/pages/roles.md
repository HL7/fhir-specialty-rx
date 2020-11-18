###  System Roles

#### Requesting System

In the Specialty Rx workflow, the Requesting System is one used by a stakeholder who participates in fulfilling specialty medication prescriptions. It may be a pharmacy system or a system used by another party such as a specialty Hub or pharmaceutical manufacturer.

A Requesting System...

- enables staff to request patient information from the prescriber's electronic health record (EHR) system using [RESTful searches](request-queries.html) or a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html))
- if supporting Specialty Rx messaging, receives [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) and [Specialty Rx Query Response - Unsolicited](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) messages
- enables staff to ask additional questions or request supporting information requiring human attention by prompting an EHR user to launch and interact with a SMART application, using a [Specialty Rx SMART Launch Task](StructureDefinition-specialty-rx-task-smart-launch.html).

#### Data Source System

The responding system in the Specialty Rx workflow is the EHR system used by the prescriber of the specialty medication or associated staff.

The Data Source system typically will...

- ***If supporting RESTful data source interactions:*** Respond to RESTful patient matching and search requests based on data stored in the patient's electronic chart
- ***If supporting Specialty Rx messaging:*** Respond systematically when a [Specialty Rx Query message](StructureDefinition-specialty-rx-bundle-query.html) is received, returning a [Specialty Rx Query Response](StructureDefinition-specialty-rx-bundle-query-response.html) based on data stored in the patient's electronic chart. It may also send [Specialty Rx Query Response - Unsolicited](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) messages proactively when a prescription is written
- Enable staff to respond to additional questions or supporting information requests that require human attention by accepting a [Specialty Rx SMART Launch Task](StructureDefinition-specialty-rx-task-smart-launch.html) and then prompting an EHR user to launch and interact with the requester's SMART application.

#### Intermediary System

An Intermediary System facilitates the exchange of information between other parties. This role is optional and assists with Requesting and/or Data Source system responsibilities when desired. See [Intermediary Facilitation](intermediary.html).

- In the messaging-based exchanges, an intermediary may use its knowledge of network participants and connection information to route prescriptions and other data exchanges between sources and receiving parties.
- In the intermediary-facilitated RESTful exchanges described above, the intermediary performs additional actions to enable data sources that only support RESTful interactions to interact with messaging-based partners.

<br>

###  Human Roles

#### Prescriber

The prescriber typically provides responses to information requests that require human interaction, such as clarifications to aspects of a prescription, using a Data Source System.

#### Prescriber Agent

The prescriber agent can provide responses to on behalf of the prescriber

#### Requester Staff

Pharmacy staff or others involved in fulfilling the prescription review information received from the data source and identify information needs that are submitted to the data source by their Requesting System.

<br>

