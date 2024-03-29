This profile ensures that the Task conveys the information that the EHR needs to...

- recognize the pharmacy or other party submitting the request
- associate the request with the patient and prescription
- place the task into the appropriate work queue
- display a description of the task to the user, and 
- launch the requested SMART application into the appropriate context (e.g., the questions staff need to answer)

<p></p>

#### Important elements in this profile

- **Task.identifier**
  - Represents the application context that the SMART app should launch into. It is conveyed during launch of the referenced SMART app in the `__appContext` parameter
- **Task.code**
  - Characterizes the requested user action (and directs the EHR to make the specified SMART application available for the user to launch)
- **Task.description**
  - User-directed text describing the task to be performed
- **Task.for** 
  - Reference to the patient resource that resides in the Data Source system
- **Task.requester**
  - The organization submitting the Task
- **Task.owner**
  - The prescriber
- **Task.reasonReference**
  - The prescription to which the task pertains
- **Task.input**
  - The client ID of the SMART app to be launched
  - **Task.input.type**: "smart-app-client-id"
  - **Task.input.valueIdentifier**: *(the SMART app's identifier)*
  
<p></p>

#### Using Task elements when launching the SMART application

The Task.identifier value (representing application context associated with the Task) is shared during SMART app launch within the `__appContext` parameter of the OAuth 2.0 access token response. It is conveyed in the `__appContext` parameter.
<p></p>