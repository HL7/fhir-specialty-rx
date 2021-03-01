Pharmacies and other stakeholders (referred to as "information requester" below) sometimes need information that isn't available through systematic querying of the prescriber's EHR (using the RESTful searches or Specialty Rx Query messages as described in the [Systematic Query Workflows](systematic-queries.html) section). 

For example, the information requester may need to: 

- ask if there’s a follow-up patient visit scheduled
- ask whether the prescriber intends to order a lab test that must be performed prior to the patient starting the medication
- ask the prescriber to provide a copy of a consent form that the patient completed by hand.

This implementation guide describes a method to support these situations by enabling the prescriber or staff to provide information through a SMART application launched from the EHR--prompted by a request from a Data Consumer system used by the pharmacy or other information requester.

<p></p>

### SMART Application Launch Using the Task Workflow

An information requester may host a SMART application that the prescriber or staff can launch from the EHR to view and respond to questions. Below is a scenario illustrating this approach for (a) communicating the need for information to the EHR and (b) enabling an EHR user to launch the application and complete the task.

- While working the prescription, staff at the information requester organization captures the questions they need to be answered by the prescriber. 
- The information requester's application (Data Consumer system) associates this set of questions with an identifier that will be used to pull the questions up when clinic staff launches the SMART app from the EHR.
- The Data Consumer system POSTs a [Task](StructureDefinition-specialty-rx-task-smart-launch.html) resource to the prescriber's EHR, asking it to create a staff work queue item to launch the information requester’s app and answer the questions. Included in the Task are elements that associate the request with the related prescription as well as fields containing the URL of the SMART app and the identifier needed to present the correct questions. 
- The EHR places an item based on the Task in a user work queue, and sets the Task status to `ready`. The EHR returns a `201 CREATED` response
- When the clinic staff takes action on the work queue item, the EHR…
  - launches the information requester's SMART App, sending a `launch` context parameter reflecting:

    - the `.id` of the Patient it received in the `.for` element of the Task resource--which references the Data Source system's Patient resource
    - the `Task.identifier` value--which the SMART app will use to present the right questions for the patient and medication. This value is later returned to the app in the access token response from the EHR authorization server

    For example, the EHR redirects to:

    ```
    https://my-pharmacy-smart-app.com?
       launch=123&
       iss=htttp://my-ehr.com/fhir
    ```

  - responds to the app's authorization request in the launch sequence with an OAuth 2.0 access token response that includes the Patient.id and appContext values. For example:

    ```
    {
      access_token:"secret-token-xyz",
      expires-in:"3600",
      patient:"specialty-rx-patient-1",
      appContext:"launch-context-id-01345005",
      ...
    }
    ```

  - sets the Task `status` to `in-progress`
- During this period, the Data Consumer system may poll the Task's `status` to monitor its progress. E.g., `GET [base]/Task/1135804`
- Once the questions have been completed in the SMART app, the Data Consumer system updates the Task's status to `completed`. The EHR updates the status and returns a `200 OK` response
- The Data Consumer system may also alert staff at the information requester organization and/or further process the information from the SMART app at this time.  (This guide does not provide direction on how to accomplish this step)

<p></p>

### Process flow: Task to SMART Launch

<div><p>
  <img src="high-level-task-to-launch-flow.png" style="float:none">  
    </p>
</div>
Note: If an event occurs within the Data Source system that prevents the Task from being performed, it SHOULD indicate that the request will not completed by updating Task.status to `failed` and, optionally, indicating why in `Task.statusReason`.

<p></p>

### Task Content

The [Task](StructureDefinition-specialty-rx-task-smart-launch.html) resource contains the following information needed to reference related information in the EHR and launch the SMART application:

- `Task.identifier` - This is a unique identifier representing the context of this task within the SMART application (e.g., the specific set of questions that need to be answered). It is to be conveyed during launch of the referenced SMART application in the `appContext` parameter and used by that application to direct the user to information and functions necessary to complete this task

- `Task.code` - A code that characterizes the requested user action
  - Value: `complete-app-questionnaire` (`display`: "Complete Questionnaire in SMART App")
  
- `Task.description` - Human-readable description of the task to be performed by the user. This description SHALL include the user-recognizable name of the SMART application to launch to perform the task, and SHALL state the action to be performed in the app once it's been launched.
  - Example: "Launch the My Pharmacy SMART App and complete the questionnaire."
  
- `Task.for` - A reference to the patient 

- `Task.requester` - The organization submitting the Task

- `Task.owner` - The prescriber

- `Task.reasonReference` - The prescription to which the task pertains. A human-readable description is included in `Task.display`, and specific identification is conveyed through either...
  - `Task.reasonReference.reference` - A reference to a MedicationRequest resource, or
  - `Task.reasonReference.identifier` - The prescription identifier set by the prescribing system. (Referred to as the Placer Order Number in HL7 v2 and Prescriber Order Number in NCPDP SCRIPT)
  
- `Task.input` - The location of the SMART app to be launched. `Task.input.type` contains the code, `smart-app-launch` and `Task.input.valueUrl` contains the actual endpoint URL to launch the SMART app.

*See this example of a [populated Task](Task-specialty-rx-task-smart-launch-1.html).*
<p></p>

### Populating the SMART Launch *appContext* 

The `appContext` parameter is sent to the SMART app as part of the [OAuth 2.0](https://oauth.net/2/) access token response, alongside other [SMART launch parameters](http://hl7.org/fhir/smart-app-launch/1.0.0/scopes-and-launch-context/#launch-context-arrives-with-your-access_token) when the SMART app is launched. The `appContext`  contains the value received in the `Task.identifier` value.

Example:

```
"appContext": "launch-context-id-01345005"
```

[SMART App Launch Implementation Guide](http://hl7.org/fhir/smart-app-launch/index.html)

<p></p>

### Hosting of SMART Applications

An information requester may potentially partner with an intermediary or other party to host the SMART application and perform the above process on its behalf.

<br>