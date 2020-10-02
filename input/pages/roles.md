###  System Roles

#### Requesting System

In the Specialty Rx workflow, the requesting system is used by a stakeholder that requires information to perform an activity related to a specialty medication prescription. 

The actors below may initiate a Specialty Rx request message. 

***Pharmacy***. The pharmacy system typically will:

- Receive the NewRx transaction requiring more information to be provided before it can be dispensed
- Enable staff to request additional information from the prescriber or their electronic health record (EHR) system (using a Specialty Rx Query message, Specialty Rx Questionnaire message, or RESTful interaction)

***Other Requesting Systems*** (examples include but are not limited to systems used by a specialty hub or manufacturer). These systems typically will:

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

###  Human Roles

#### Prescriber

The prescriber typically will provide responses to information requests that require human intervention, such as clarifications to aspects of a prescription.

#### Prescriber Agent

The prescriber agent can provide responses to on behalf of the prescriber

#### Requester Staff

Pharmacy staff and others involved in fulfilling the prescription review information received from the data source and identify information needs that are submitted to the data source by their requesting system.

<br>

