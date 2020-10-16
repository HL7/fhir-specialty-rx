### Information Flows Requiring Human Interaction

Pharmacies and other stakeholders sometimes need information that isn't available through systematic  querying of the prescriber's EHR (using the RESTful searches or Specialty Rx Query messages as described in the [Systematic Query Workflows](systematic-queries.html) section). 

For example, the pharmacy may need to: 

- ask the clinic to clarify the prescription's dosing instructions
- ask whether the clinic intends to order a lab test that must be performed prior to the patient starting the medication
- ask the clinic to provide a copy of a consent form that the patient completed by hand.

### Methods: SMART Application and Questionnaire

This implementation guide describes two methods to support these situations: 

- enabling the prescriber or staff to provide information through a SMART application launched from the EHR
- transmission of questions and responses containing human-gathered information using the [Specialty Rx Questionnaire](StructureDefinition-specialty-rx-bundle-questionnaire.html) and [QuestionnaireResponse](StructureDefinition-specialty-rx-bundle-questionnaire-response.html) messages.

### SMART Application Launch Using the Task Workflow

A requesting party may host a SMART application that the prescriber or staff can launch from the EHR to view and respond to questions. Below is a scenario illustrating this approach for (a) communicating the need for information and (b) enabling a person to launch the application and complete the task.

- While working the prescription, staff at the pharmacy or other requesting party captures the questions they need to be answered by the prescriber clinic. 
  - The requester's application tags the set of questions with an identifier that will be used to pull up the right questions when clinic staff launches the SMART app from the EHR.
- The requesting system exchanges a [Task](StructureDefinition-specialty-rx-task-smart-launch.html) resource with the prescriber's EHR, asking it to create a staff work queue item to launch the requester’s app and answer the questions. Included in the Task are elements that associate the request with the related prescription as well as fields containing the URL of the SMART app and the identifier needed to present the correct questions. 
- When the clinic user takes action on the work queue item, the EHR…
  - launches the requester's SMART App
  - sets a session launch context using the patient ID it received in the `.for` element of the Task resource 
  - includes the `Task.identifier` value in the `appContext` launch parameter… which the SMART app uses to pull up the right patient/medication questions.

#### Task Content Overview

The [Task](StructureDefinition-specialty-rx-task-smart-launch.html) resource contains the following information needed to reference related information in the EHR and launch the SMART application:

- `Task.identifier` - This is a unique identifier representing the context of this task (e.g., the specific set of questions that need to be answered). It is to be conveyed during launch of the referenced SMART application (within the `appContext` parameter, as `initiationId`) and used by that application to direct the user to information and functions necessary to complete this task

- `Task.code` - A code that characterizes the requested user action
  - Value: "complete-app-questionnaire" (display: "Complete Questionnaire in App")
  
- `Task.description` - Human-readable description of the task to be performed by the user. This description must include the user-recognizable name of the SMART application to launch to perform the task, and must state the action to be performed in the app once it's been launched.
  - Example: "Launch the My Pharmacy SMART App and complete the questionnaire."
  
- `Task.focus` - The prescription to which the task pertains. A human-readable description is included in `Task.display`, and specific identification is conveyed through either...
  - `Task.focus.reference` - A reference to a MedicationRequest resource, or
  - `Task.focus.identifier` - The prescription identifier set by the prescribing system. (Referred to as the Placer Order Number in HL7 v2 and Prescriber Order Number in NCPDP SCRIPT)
  
- `Task.for` - A reference to the patient 

- `Task.requester` - The organization submitting the Task

- `Task.owner` - The prescriber

- `Task.input` - The location of the SMART app to be launched. `Task.input.type` contains the code, "smart-app-launch" and `Task.input.valueUrl` contains the actual endpoint URL to launch the SMART app.

*See this example of a [populated Task](Task-specialty-rx-task-smart-launch-1.html).*

#### Populating the SMART Launch *appContext* 

The `appContext` parameter is sent to the SMART app as part of the [OAuth 2.0](https://oauth.net/2/) access token response, alongside other [SMART launch parameters](http://hl7.org/fhir/smart-app-launch/1.0.0/scopes-and-launch-context/#launch-context-arrives-with-your-access_token) when the SMART app is launched. The `appContext`  contains an `initiationId` field populated with the value received in the `Task.identifier` value.

Example:

```
"appContext": {"initiationId": "05d06540dd00d"}
```

[SMART App Launch Implementation Guide](http://hl7.org/fhir/smart-app-launch/index.html)

<br>

#### Process flow: Task to SMART launch

<div><p>
  <img src="high-level-task-to-launch-flow.png" style="float:none">  
    </p>
</div>

<br>

### Specialty Rx Questionnaire Messages

This guide also defines FHIR message profiles enabling:

- a Requesting System to convey a set of questions or information requests to the Data Source System using a Questionnaire resource ([Specialty Rx Questionnaire message](StructureDefinition-specialty-rx-bundle-questionnaire.html))
- a Data Source System to engage an EHR user to collect information requested by the questionnaire and  return it in a [Specialty Rx Questionnaire Response message](StructureDefinition-specialty-rx-bundle-questionnaire-response.html).

This approach is suited to stakeholders whose system environments and relationships better support a messaging model--for example those that typically exchange electronic prescriptions using an intermediary.

<h3>Intermediary Facilitation Between Messaging and Task Models</h3>

In situations where the requesting party prefers a messaging model, an intermediary can mediate between messaging on the Requester side and a Task model on the Data Source side. 

<div><p>
  <img src="high-level-facilitated-task-flow.png" style="float:none">  
    </p>
</div>

<br>