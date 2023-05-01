The profile...

- requests consent or authorizations to support fulfillment of a prescribed specialty product 
- provides the appropriate consent form for the prescribed product

<p></p>

**Important elements in this profile:**

- **Task.status**: "requested"
- **Task.code**: "obtain-consent"
  - Characterizes the requested user action (and directs the EHR to make the consent form referenced in Task.input available to the user)
- **Task.description**
  - User-directed text describing the task to be performed
  - e.g., "Have the patient complete the attached consent form and capture a PDF of the signed form in a Consent"
- **Task.for**
  - Reference to the patient resource that resides in the Data Source system
- **Task.requester**
  - The organization submitting the Task
- **Task.owner**
  - The prescriber
- **Task.reasonReference**
  - The prescription to which the task pertains
- **Task.input**
  - A reference to a Consent resource containing the consent form that is appropriate for the prescribed product
  - **Task.input.type**: "consent-form-reference"
  - **Task.input.valueReference**: *reference to the blank consent form*
- **Task.output (populated when the Task status is set to "completed")**
  - A reference to a Consent resource containing a consent form that has been completed
  - **Task.output.type**: "completed-consent-reference"
  - **Task.output.valueReference**: *reference to the completed consent form*

  
<p></p>
