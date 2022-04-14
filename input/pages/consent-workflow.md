intro text

<p></p>


### Background: Specialty Product Consents, Roles and Process
Consents and authorizations supporting fulfillment of a specialty medication or other specialty product typically:
* are separate from consents obtained by the clinic or health system at which the specialty product order is being ordered
* may be between the patient and a specialty pharmacy, manufacturer or patient support organization ("specialty HUB") for services and interactions not covered by general treatment and healthcare operations consent rules
* include multiple aspects including release of clinical information, sharing of financial information, permission to be contacted by text message or other means, participation in research, etc.
* are obtained using "enrollment" consent forms that are specific to the brand product being ordered, containing mutliple provisions using wording that is unique to the product or manufacturer
* are typically obtained from the patient with the assistance of staff at the clinic where the product is ordered, who locate the appropriate form to be signed by the patient and transmit it to the manufacturer, pharmacy or specialty HUB)
* may include authorizations or certifications from the prescriber related to the patient's conditions, previous care and proposed therapy.

Depending on a provider's specialty, completion of product consents may be a frequent step in patient care or a less common activity. Practices that prescribe a large number of specialty products may have processes in place to flag when enrollment consent forms must be completed and which particular form is appropriate to the prescription. But for those practices that prescribe fewer specialty products, knowing when consent is required and locating the correct form can be challenging and a cause of delays in getting the product to the patient.

<p></p>

### IG Support for Industry Conventions
This guide aims to provide methods for sharing specialty product consents that are compatible with current industry conventions regarding
* the types of consents needed for product fulfillment and patient support
* the roles played by stakeholders in obtaining, sharing and maintaining consents
* the form in which consent is given by the patient, which today is typically on paper.

The consent content and workflow processes described in this guide accommodate the product-specific nature of current enrollment forms by:
* enabling practices with established product consent processes to transmit the completed consents at the same time as the product order
* providing a means for a pharmacy or other party to request consent if not supplied with the product owner
* enabling the requesting party to provide the correct enrollment consent form for the prescribed product
* enabling the consent form to be signed on paper as is typical today and to be transmitted as a scanned electronic attachment embedded in the FHIR Consent resource.

The guide also seeks to enable improvement of current processes through support for optional features including transmission of electronic signatures and capturing of discrete information related to the consent.

<p></p>

### Exchange Workflow Options: Proactive Message, Task and SMART App 
The guide defines three methods for requesting and exchanging consents associated with prescribed specialty products:

1. **Task-based Consent request.** The pharmacy or other Data Consumer posts a Task to the prescriber system (Data Source) requesting that consent be obtained from the patient and made available in a Consent resource. The Data Consumer polls the Data Source and retrieves the Consent resource once it is available. 
2. **Task-initiated SMART App Launch.** The pharmacy or other Data Consumer system uses the [Specialty Rx SMART Launch Task](StructureDefinition-specialty-rx-task-smart-launch.html) process to prompt staff at the prescriber clinic to use a SMART app to obtain and return the appropriate consent form for the prescribed product.
3. **Unsolicited Message.** The prescribing system can transmit the consent at the time of product order using using this guide's [Specialty Rx Query Response - Unsolicited](StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html) profile. The Consent resource is included alongside other clinical and insurance information associated with the prescription.

<p></p>

The sections below further describe each option.

<p></p>

### Process flow: Task-based Consent Request
A pharmacy or other fulfilling party can request needed consent information using the standard FHIR Task workflow process. 

In this process: 
* the requesting system (Data Consumer) POSTs a Task containing the required consent form to the prescriber system (Data Source)
* the Data Source system places a task into a staff work queue in a way that makes the consent form available to be downloaded and signed by the patient,  and sets the Task status to `ready`. The EHR returns a `201 CREATED` response
* the signed consent is captured in a [Specialty Rx Consent](StructureDefinition-specialty-rx-consent.html) resource
* the Data Source updates the Task as `completed` and adds a reference to the completed Consent in the `Task.output` element
* During this period, the Data Consumer system polls the Task's `status` to monitor its progress. E.g., `GET [base]/Task/1135804`
* The Data Consumer retrieves the completed Consent when it becomes available. E.g., `GET [base]/Consent/12340654`

<p></p>

<div><p>
  <img src="high-level-task-consent-request-flow.png" style="float:none">  
    </p>
</div>

<p></p>

Notes: 
* [Specialty Rx Task - Consent Request profile](StructureDefinition-specialty-rx-task-consent-request.html)
* Example of a [consent request Task--upon submission to the Data Source (request)](Task-specialty-rx-task-consent-request-1.html)
* Example of a [consent request Task--after patient has completed the consent form (response)](Task-specialty-rx-task-consent-request-2-completed.html)
* This method is based on the FHIR workflow management option [POST of Task to fulfiller's system](https://www.hl7.org/fhir/workflow-management.html#optiong).

<p></p>

When utilizing this method to obtain consent, a reference to the appropriate consent form to be completed (a [Specialty Rx Consent - Requested](StructureDefinition-specialty-rx-consent-requested.html)) is included in the Task's `.focus` element.

Note: If an event occurs within the Data Source system that prevents the Task from being performed, it SHOULD indicate that the request will not completed by updating Task.status to `failed` and, optionally, indicating why in `Task.statusReason`.

<p></p>

### Process flow: Task to SMART Launch
A pharmacy or other fulfilling party may optionally request consent information through use of a SMART application as defined in the [Information Flows Requiring Human Interaction](human-interaction.html) section. 

This method prompts staff at the prescriber clinic to: 
* launch a SMART app
* download and have the patient complete the product-specific consents
* and then upload the completed form to the SMART app.

When using this method to obtain consents, the [Task](StructureDefinition-specialty-rx-task-smart-launch.html) resource is populated as described in [this section](human-interaction.html#task-content).

<p></p>

### Process flow: Unsolicited Message
When the prescribing practice has internal processes in place to obtain consents up-front during the ordering process, it can record the result as a [Specialty Rx Consent](StructureDefinition-specialty-rx-consent.html) resource and include it with other pertinent patient information in an unsolicited FHIR message to fulfilling parties at the same time that it transmits the order. This process is described in the [Systematic Query Workflows section](systematic-queries.html#unsolicited-workflow-overview).
 

<br>