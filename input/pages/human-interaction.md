### Information Flows Requiring Human Interaction

Pharmacies and other stakeholders sometimes need information that isn't available through systematic  querying of the prescriber's EHR (using Query messages and RESTful searches described in the Workflow section). 

For example, the pharmacy may need to: 

- ask the clinic to clarify the prescription's dosing instructions
- ask whether the clinic intends to order a lab test that must be performed prior to the patient starting the medication
- ask the clinic to provide a scan of a form that the patient completed by hand.

### Methods: Questionnaire and SMART Application

This implementation guide describes two methods to support these situations: 

- transmission of questions and human-gathered information using the Specialty Rx Questionnaire Request and Response message
- enabling the prescriber or staff to provide information through a SMART application launched from the EHR.

### Specialty Rx Questionnaire Messages

This guide defines FHIR message profiles enabling:

- a Requesting System to convey a set of questions or information requests to the Data Source System using a Questionnaire resource
- a Data Source System to engage an EHR user to collect information requested by the questionnaire and  return it in a QuestionnaireResponse message.

<br>

### SMART Application Launch Using the Task Workflow

A requesting party may provide a SMART application that the prescriber or staff can launch from the EHR to view and respond to questions. Below is a scenario illustrating the strategy for communicating the need for information and enabling a person to launch the application.

- While working the prescription, staff at the pharmacy or other requesting party captures the questions they need to be answered by the prescriber clinic. 
  - The requester's application tags the set of questions with an *“Initiation ID”* that will be used to pull up the right questions when clinic staff launches the SMART app from the EHR 
- The requesting system exchanges a Task resource with the prescriber's EHR, asking it to create a staff work queue item to launch the requester’s app and answer the questions. 
  - Included in the Task are: identification of the SMART app, the patient ID and the *“Initiation ID”* for pulling up the questions
- When the clinic user takes action on the work queue item, the EHR…
  - launches the requester's SMART App
  - sets a session launch context using the patient ID it received in the Task
  - includes the *“Initiation ID”* in the *appContext* launch parameter… which the SMART app will use to pull up the right patient/medication questions.

#### Populating the Initiation ID reference in the SMART launch *appContext* 

*From: [CDS Hooks Sep 2020 Ballot](https://cds-hooks.hl7.org/ballots/2020Sep/):*

The `appContext` field and value will be sent to the SMART app as part of the [OAuth 2.0](https://oauth.net/2/) access token response, alongside the other [SMART launch parameters](http://hl7.org/fhir/smart-app-launch/1.0.0/scopes-and-launch-context/#launch-context-arrives-with-your-access_token) when the SMART app is launched. Note that `appContext` could be escaped JSON, base64 encoded XML, or even a simple string, so long as the SMART app can recognize it.

Example:

```
 "appContext": "{\"initiationId\":3456356,\"settings\":{\"module\":4235}}"
```

[SMART App Launch Implementation Guide](http://hl7.org/fhir/smart-app-launch/index.html)

<br>

### SMART App Launch During the Prescribing Process - Using CDS Hooks

... [to be added]

<br>