<blockquote class="note-to-balloters">
<p>
This version of the IG includes new content to support requesting and sharing consents that are frequently needed when fulfilling specialty product prescriptions. 
<br/><br/>
<i>Additions in version 1.1.0 (STU2 ballot)</i><br/>
<ul>
<li><a href="consent-workflow.html">Consent workflows</a> gives an overview of consent scenarios supported by the guide.</li>
<li><a href="StructureDefinition-specialty-rx-consent-requested.html">Requested consent profile conveying the appropriate blank consent form</a></li>
<li><a href="StructureDefinition-specialty-rx-consent.html">Consent profile for completed specialty consents</a></li>
<li><a href="StructureDefinition-specialty-rx-task-consent-request.html">Task profile used to request consent.</a>. This profile is used in an exchange process based on the FHIR workflow management option <a href="https://www.hl7.org/fhir/workflow-management.html#optiong">POST of Task to fulfiller&#39;s system</a>.</li>
<li>Terminology:
<ul>
<li>New value in the specialty-rx-task-type <a href="CodeSystem-specialty-rx-task-type.html">code system</a> and <a href="ValueSet-specialty-rx-task-type.html">value set</a></li>
<li>New value in the specialty-rx-task-input-type <a href="CodeSystem-specialty-rx-task-input-type.html">code system</a> and <a href="ValueSet-specialty-rx-task-input-type.html">value set</a></li>
<li>New specialty-rx-task-output-type <a href="CodeSystem-specialty-rx-task-output-type.html">code system</a> and <a href="ValueSet-specialty-rx-task-output-type.html">value set</a></li>
</ul>
</li>
<li>New examples: </li>
<ul>
<li><a href="Consent-specialty-rx-consent-requested-1.html">Requested Consent resource (containing a blank consent form)</a></li>
<li><a href="Consent-specialty-rx-consent-1.html">Completed Consent resource</a></li>
<li><a href="Task-specialty-rx-task-consent-request-1.html">Task illustrating a consent request</a></li>
<li><a href="Task-specialty-rx-task-consent-request-2-completed.html">Completed Task after consent is obtained</a></li>
</ul>
</ul>
</p>
</blockquote>

<p></p>
<p></p>

### Overview
This FHIR implementation Guide describes the exchange of patient demographic, clinical and coverage data to support fulfillment of specialty medication prescriptions by pharmacies, and enrollment of patients into related support programs offered by parties such as Hub vendors and pharmaceutical manufacturers.

This guide is the result of collaboration between HL7 and the National Council for Prescription Drug Programs (NCPDP).

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
- [Consent Workflows](consent-workflow.html) gives an overview of consent scenarios supported by the guide.
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
		<td colspan="2">HL7 Pharmacy Workgroup</td>
  	  </tr>
	  <tr>
		<td colspan="2">NCPDP Workgroup 18 - Specialty Requirements for ePrescribing Taskgroup</td>
  	  </tr>
	  <tr>
		<td>Frank McKinney</td>
		<td><a href="mailto:frank.mckinney@pocp.com">frank.mckinney@pocp.com</a></td>
	  </tr>
	</tbody>
  </table>



