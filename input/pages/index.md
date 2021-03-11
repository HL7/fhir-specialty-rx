### Overview
This FHIR implementation Guide describes the exchange of patient demographic, clinical and coverage data to support fulfillment of specialty medication prescriptions by pharmacies, and enrollment of patients into related support programs offered by parties such as Hub vendors and pharmaceutical manufacturers.

This guide is co-branded between HL7 and the National Council for Prescription Drug Programs (NCPDP).

### Background

The current process for exchanging information to support specialty medication fulfillment is complex and manual, often resulting in delays of days to weeks before patients can begin their therapy. This is caused largely by the absence of an industry standard for exchanging clinical data needed to dispense specialty medications and enroll the patient into associated support and savings programs.

NCPDP created a task group to focus on the exchange of this data, with the goal of reducing the time to therapy for a patient who has been prescribed a specialty medication. The group identified demographic, clinical and coverage information needed to support the process, and defined data exchange workflows between the clinic, pharmacy and other fulfilling parties to efficiently deliver the data to the parties that need it.

This information is outside of the scope of the NCPDP e-prescription standard that conveys specialty orders to pharmacies in the US today. After an extensive analysis of the types of information required beyond what is carried in the prescription, the task group determined that developing an implementation guide using HL7 FHIR would be the best approach for meeting this need. Exchange of that information is the focus of this guide. 

### Scope of This Guide

This guide addresses the exchange of information to support specialty medication fulfillment functions, including:

- medication dispensing and billing
- specialty enrollment for programs or services
- facilitation of clinical care management, education, and training.

The guide does not address transmission of the original prescription from the prescriber to dispensing pharmacy, which is typically accomplished in the US using the NewRx message defined in the NCPDP SCRIPT standard. 

Further, the exchanges described in the guide are not intended to be used to request a change to a received prescription or to propose a particular clarification; these functions are supported by the NCPDP SCRIPT RxChangeRequest and RxChangeResponse messages.

This implementation guide is intended be used in the United States. It reflects US pharmacy processes and conventions.

### Content and Organization

The guide is organized into the following sections:

- [Use Cases and Roles](roles.html) gives an overview of the guide's goals and participants.
- [Systematic Query Workflows](systematic-queries.html) describes the exchanges that retrieve information systematically from the patient's records.
- [Information Flows Requiring Human Interaction](human-interaction.html) describes a process enabling the prescriber or staff to provide information through a SMART application launched from the EHR.
- [Search Conventions](searches.html) defines required and recommended searches and conventions for specifying searches in Specialty Rx messages.
- [Patient Matching](patient-matching.html) describes methods for identifying the patient for whom information is being exchanged.
- [Message Structures](message-structure.html) and [Message Submission](message-submission.html) give details related to the Specialty Rx messaging options.
- [Error Handling](error-handling.html) defines expectations for handling exception situations.
- [Conformance Expectations](missing-data.html) defines use of Must Support elements and also describes conventions for situations where information is not available.
- [Intermediary Facilitation](intermediary.html) describes how an intermediary can enable exchange between implementers of the guide's RESTful and messaging options.
- [Security](security.html) provides information for implementers related to security and privacy.
- [Specialty Rx Profiles, Terminology and Examples](artifacts.html) lists all profiles and terminology defined in this guide. It also provides examples instances that conform to the guide's profiles.
- [Applicable US Core Profiles](us-core-profiles.html) defines expectations for the use of US Core profiles in the guide's searches.
- [Capability Statements](capability-statements.html) defines sets of guide functionality that can be implemented individually or in combination.

### FHIR Basics 

For those new to FHIR, the material below describes basic FHIR principles and gives guidance for reading FHIR specifications.

- [FHIR overview](http://hl7.org/fhir/R4/overview.html)
- [Developer’s introduction](http://hl7.org/fhir/R4/overview-dev.html) (or [Clinical introduction](http://hl7.org/fhir/R4/overview-clinical.html))
- [FHIR data types](http://hl7.org/fhir/R4/datatypes.html)
- [Using codes](http://hl7.org/fhir/R4/terminologies.html)
- [References between resources](http://hl7.org/fhir/R4/references.html)
- [How to read resource & profile definitions](http://hl7.org/fhir/R4/formats.html)
- [Base resource](http://hl7.org/fhir/R4/resource.html)

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

### Change Log

  <table class="grid">
    <tbody>
	  <tr>
		<td>Date</td>
		<td>Change</td>
  	  </tr>
	  <tr>
		<td>Feb 11, 2021</td>
		<td>Corrected approved typo fixes, proposed adjustments for FHIR-30595, 30597, 30627 and 30628. Revision in-process on Search Conventions page</td>
  	  </tr>
	  <tr>
		<td>Feb 15, 2021</td>
		<td>Completed proposed changes to Search page and CapabilityStatements to address comments FHIR-30484, FHIR-30485, FHIR-30486, and FHIR-30608. Replaced parameter examples with links to related US Core specification, added guidance and examples for _revinclude and _include parameter usage, adjusted search example to match US Core required parameter combination for MedicationRequest, added _revinclude requirements to capability statements and added a 'SHALL follow US Core search guidance' statement and link to the Search Conventions page to all CapabilityStatement pages and 'SHALL follow US Core search' to all CapabilityStatement rest documentations sections. <br/>Changed Data Recipient to Data Consumer in Capability Statement narratives, CapabilityStatement names and Search Conventions page content in response to comment FHIR-30610 (additional IG changes for 30610 are yet to be made)</td>
  	  </tr>
	  <tr>
		<td>Feb 19, 2021</td>
		<td>Applied the remaining “data requester”/”data recipient” to “consumer” wording changes to narrative pages (MessageDefinition-specialty-rx-query intro, StructureDefinition-specialty-rx-bundle-query intro, StructureDefinition-specialty-rx-bundle-search-result intro, Task-specialty-rx-task-smart-launch-2-ids intro, Flows Requiring Human Interaction, Intermediary Facilitation, Message Structure, Conformance Expectations, Patient Matching, Use Cases and Roles, Systematic Queries, Capability Statements, Message Submission). Changed the names of the pharmacy capability statements to Data Consumer and adjusted the narrative pages to match. Added _revinclude/Provenance entries to the capability statements to match US Core. Added a statement to the capability statements and narrative pages saying that implementing systems SHALL follow US Core search requirements and guidance when performing searches associated with this guide. Added a link to the Search Conventions section on the capability statement narrative pages. Corrected links on the Search Convention and Security pages. Adjusted statements in Message Submission and Systematic Queries related to synchronous/asynchronous processing to refer to the definition in the $process-message operation (removed prohibition on use of the async parameter)</td>
  	  </tr>
	  <tr>
		<td>Feb 26, 2021</td>
		<td>Addressed ballot comments related to: prescriber/clinic/staff wording on the Flows Requiring Human Interaction page; changing use of Backend Services Authorization to SHOULD on the Security page and capability statements. </td>
  	  </tr>
	  <tr>
		<td>Mar 1, 2021</td>
		<td>Addressed ballot comments related to the Task-to-SMART lauch process: FHIR-30604, FHIR-30605, FHIR-30606, FHIR-30607</td>
  	  </tr>
	  <tr>
		<td>Mar 2, 2021</td>
		<td>Applied resolution to FHIR-30606 (change the primary SMART App identifier in the IG's Task profile, specialty-rx-task-smart-launch, to SMART APP Client ID and make the existing SMART App URL optional. Add a new value to the code system, specialty-rx-task-input-type to represent the added Client ID option. Apply additional wording to the Task profile and exmample to clarify that the Task.for element specifically reflects the Data Source's patient</td>
  	  </tr>
	  <tr>
		<td>Mar 9, 2021</td>
		<td>Applied additional comment resolutions</td>
  	  </tr>
	  <tr>
		<td>Mar 10, 2021</td>
		<td>Applied comment resolution for FHIR-30427 - change wording in profile intro for specialty-rx-bundle-search-results, removing unnecessary / confusing first sentence. Adjusted the specialty-rx-bundle-search-result profile narrative to describe population of the Bundle.link elements according to FHIR search response guidelines.</td>
  	  </tr>
   </tbody>
  </table>

<br />
















