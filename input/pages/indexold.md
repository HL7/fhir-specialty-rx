### Overview
This FHIR implementation Guide describes the exchange of data (demographic, prescription, clinical and financial) for dispensing specialty medications by pharmacies as well as facilitating enrollment of patients in programs offered by third parties such as, but not limited to, Hub vendors and Pharmaceutical manufacturers.

This guide is co-branded between HL7 and the National Council for Prescription Drug Programs (NCPDP)

### Background

The current process for exchanging data, including prescription data regarding specialty medications, is complex and manual, taking days to weeks to begin a patient on therapy. 

There is no industry standard for exchanging clinical data when necessary for dispensing specialty medications by pharmacies--as well as facilitating enrollment of patient in programs offered by third parties such as Hub vendors or Pharmaceutical Manufacturers. 

NCPDP started a task group several years ago focused on the exchange of data needed to help shorten the time to therapy for a patient who has been prescribed a specialty medication and over the past two years have been focused on identifying demographic, clinical and financial information that needs to be exchanged in order to get the patient the therapy they need. 

This information is outside of the current e-Prescription that is sent to the pharmacy today. After an extensive analysis of the types of additional information that is required along with the prescription it was determined that developing an implementation guide using HL7 FHIR would be the best approach to support the exchange of this information. 

### Scope of this guide

This guide is intended be used in the United States. It reflects US pharmacy processes and conventions.

The implementation guide supports business functions related to fulfillment of specialty medication prescriptions, such as:

- Request of additional information to facilitate medication dispensing and billing.
- Specialty enrollment for programs or services.
- Facilitation of clinical care management, education, and training

### Authors

  <table class="grid">
    <tbody>
	  <tr>
		<td>HL7 Pharmacy Workgroup</td>
		<td></td>
  	  </tr>
	  <tr>
		<td>NCPDP Workgroup 18</td>
		<td>Specialty Requirements for ePrescribing Taskgroup</td>
  	  </tr>
	  <tr>
		<td>Frank McKinney</td>
		<td><a href="mailto:frank.mckinney@pocp.com">frank.mckinney@pocp.com</a></td>
	  </tr>
	</tbody>
  </table>

### Change log
  <table class="grid" style="width:100%">
      <colgroup><col span="1" style="width:150px"><col></colgroup> 
    <tbody>
	  <tr>
		<td>Mar 20, 2020</td>
		<td>Initial structure and content</td>
  	  </tr>
  	  <tr>
		<td>Apr 6, 2020</td>
		<td>Additional content: Workflow page, refined profiles and examples for MedicationRequest, Patient, Practitioner, Condition, AllergyIntolerance </td>
  	  </tr>
  	  <tr>
		<td>Apr 7, 2020</td>
		<td>Additional content: profiles and examples for PractitionerRole, Endpoint, Organization, Location</td>
  	  </tr>
  	  <tr>
		<td>Apr 10, 2020</td>
		<td>Additional content: profiles and examples for Provider-Organization, Payor-Organization, Observation, RelatedPerson, CareTeam, Consent, Provenance</td>
  	  </tr>
  	  <tr>
		<td>Apr 24, 2020</td>
		<td>Additional content: profiles and examples related to request and response using the CDex profile (CommunicationRequest, Communication, request and response Bundles, additional Organization example for the pharmacy). <br><b>Notes:</b><br> <ul>
            <li>Investigating challenges conforming to CDex Communication profile... specifically the Communication.basedOn element's slicing to require the basedOn resource to conform to CDex Communication. Currently using an IG-defined Communication profile that adjusts the basedOn slicing discriminator to basedOn.resolve().</li><li>Encountering build error in specialty-rx-response-bundle-1, also related to Communication.basedOn, if the CommunicationRequest is not included in the bundle (and it probably shouldn't be included). Investigating</li>
            </ul></td>
  	  </tr>
       <tr>
		<td>May 1, 2020</td>
		<td>Additional example content including an unsolicited standard Specialty Rx Bundle containing current medications, allergies, conditions and vitals. Refined existing examples</td>
  	  </tr>
      <tr>
		<td>May 12, 2020</td>
		<td>Added event-type code system and value set. Cleaned up narrative wording. Corrections.</td>
  	  </tr>
        <tr>
		<td>May 14, 2020</td>
		<td>Added messaging detail: Request and response MessageDefinition, MessageHeader, and Bundle profiles. Added intial CapabilityStatements. Refined examples to reference messaging profiles. Added Message Submission page. 
<br/>Noted in-process clinical profiles that currently have no constraints beyond US Core (which will be removed if the workground determines the associated US Core profiles can be use as-is). Other refinements.</td>
  	  </tr>
      <tr>
		<td>June 16, 2020</td>
		<td>Changes...
            <ul>
              <li>added guidance page describing patient matching and request/response processing detail</li>
              <li>added guidance page describing request query strings</li>
              <li>added CommunicationRequest resource that further constrains the CDex profile. Specifically limits the .about element to contain the responding system's Patient resource and/or the related MediationRequest and clarify population of subject</li>
              <li>refined CommunicationRequest resource to limit the .about element to contain the requesting system's Patient resource and/or the related MediationRequest and clarify population of subject</li>
              <li>added ValueSet constraining the US Core Condition Code (removing ICD-9-CM)and binding w/in the Condition profile</li>
              <li>added CodeSystem and ValueSet for communication categories used in the Communication and CommunicationResponse</li>
              <li>added Coverage profile (and example resource) that identifies pertinent elements to identify pharmacy and medical coverage</li>
              <li>Adjusted example file references so that they appear on profile pages</li>
            </ul>
		</td>
  	  </tr>
      <tr>
		<td>June 30, 2020</td>
		<td>Removed dependencies on Da Vinci CDex and HRex profiles. Added new operation and messaging approach for team review</td>
  	  </tr>
      <tr>
		<td>July 13, 2020</td>
		<td>Reorganized and fleshed out message approaches: (a) event-type with Parameters as focus, (b) invoke operation.</td>
  	  </tr>
      <tr>
		<td>July 20, 2020</td>
		<td>Refined message structure and naming. Removed content associated with alternate models.</td>
  	  </tr>
      <tr>
		<td>July 21, 2020</td>
		<td>Adjustments to guidance to match adjusted message structures.</td>
  	  </tr>
      <tr>
		<td>July 23, 2020</td>
		<td>Cleaned up resource naming. Adjusted patient and parameters profiles. Added rough questionnaire and questionnaire response messages and components</td>
  	  </tr>
        <tr>
		<td>July 27, 2020</td>
		<td>Added a page outlining the message structures. Added clarification to the Search Conventions page that Patient references within searchset bundles in the Query Response should resolve to the responder-patient resource in the response's main message bundle</td>
  	  </tr>
      <tr>
		<td>July 28, 2020</td>
		<td>Added unsolicited data message (Query Response - Unsolicited) and associated structures and example. Updated page outlining the message structures. Updated Workflows page graphics - unsolicited flow. Updated Workflow Scenarios and Message Submission . Several s adjustments to examples. Added illustrations to message examples</td>
  	  </tr>
      <tr>
		<td>July 31, 2020</td>
		<td>Added query error profiles and examples for fatal response error and individual search error. Renamed proactive-data profiles to query-response-unsolicited. Added error handling page</td>
  	  </tr>
      <tr>
		<td>Aug 2, 2020</td>
          <td>Changed name of <i>query-response-error</i> event and related message resources and examples to <i>query.</i> Added more specifics to the Error Handling page. Linked examples into structure definition pages</td>
  	  </tr>
      <tr>
		<td>Aug 18, 2020</td>
          <td>Remove resource profiles that did not expand materially on US Core. Reference the associated US Core profiles: AllergyIntolerance, CareTeam, Location, Lab Observation</td>
  	  </tr>
      <tr>
		<td>Aug 21, 2020</td>
          <td>Add RESTful data source model, enabling data sources to participate in the exchange solely through RESTful operations (facilitated by an intermediary when needed). Updated the Workflows page and added a Data Source - RESTful CapabilityStatement</td>
  	  </tr>
      <tr>
		<td>Aug 24, 2020</td>
          <td>Added a separate page to identify US Core resources expected to be used in Specialty Rx exchanges</td>
  	  </tr>
      <tr>
		<td>Oct 1, 2020</td>
          <td>Separated role information into its own Roles page. Focused the previous Workflows page on systematic data retrieval--reorganizing/revising it and and renaming it Systematic Query Workflows. Added a page that focuses on requests that require human intervention, titled Information Flows Requiring Human Interaction, that discusses use of the Questionnaire messages and use of SMART apps and CDS Hooks.</td>
  	  </tr>
      <tr>
		<td>Oct 7, 2020</td>
          <td>Added Task profile that defines content enabling a pharmacy or other external party to prompt clinic staff to launch a SMART app and answer prescription-related questions. Added CodeSystem and ValueSet defining a task type meaning "complete a questionnaire using the referenced SMART application". Adjusted the page, Flows Requiring Human Intervention: removed CDS Hooks placeholder. Added clarification to the Mesage Submission page specifying that the requesting system cannot influence whether the response is returned synchronously or asynchronously; the data source system determines this for each request.</td>
  	  </tr>
      <tr>
		<td>Oct 8, 2020</td>
          <td>Added example Task that prompts clinic staff to launch a SMART app and answer prescription-related questions. </td>
  	  </tr>
	<tr>
		<td>Oct 13, 2020</td>
          <td>Added exchange flows and additional content to the Information Flows Requiring Human Interaction page. Refined example resource illustration format throughout and added content illustrations to all examples. Added descriptive content to the Specialty Rx Task example page. </td>
        </tr>
	<tr>
		<td>Oct 15, 2020</td>
          <td>Reorganized and revised the Systematic Query Workflows page to better cover both RESTful and messaging-based workflows</td>
        </tr>
	<tr>
		<td>Oct 16, 2020</td>
          <td>Removed Questionnaire messaging resources and associated narrative. Clarifying edits to the human-interaction workflow guidance page. </td>
        </tr>
	<tr>
	   <td>Oct 18, 2020</td>
          <td>Refined example presentation - added expandable view of bundled resources </td>
        </tr>
	<tr>
	   <td>Oct 26, 2020</td>
          <td>Removed Questionnaire / Questionnaire response message details from the Message Structures guidance page</td>
        </tr>
	<tr>
	   <td>Oct 29, 2020</td>
          <td>Added a guidance page covering handling for missing Must Support and Required data elements. Added example Pharmacy Organization with missing required telecom element.</td>
        </tr>
   </tbody>
</table>



<br />
















