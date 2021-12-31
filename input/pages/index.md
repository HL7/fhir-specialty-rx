### *New Consent-Releated Content in Draft STU2 Version*  

This draft STU2 version of the IG includes new content to support requesting and sharing patient consents related to fulfillment of the prescribed specialty product. This content is in-process and subject to change based on stakeholders' input.

#### *Additions in this draft STU2 version*
- [Patient Consent Workflows](consent-workflow.html) gives an overview of consent scenarios supported by the guide.
- [Requested Consent profile conveying the appropriate blank consent form](StructureDefinition-specialty-rx-consent-requested.html)
- [Consent profile for provided patient consents](StructureDefinition-specialty-rx-consent.html)
- [Task profile used to request consent.](StructureDefinition-specialty-rx-task-consent-request.html). This profile is used in an exchange process based on the FHIR workflow management option [POST of Task to fulfiller's system](https://www.hl7.org/fhir/workflow-management.html#optiong).
- Terminology:
	- New value in the [specialty-rx-task-type](ValueSet-specialty-rx-task-type.html)
	- New value in the specialty-rx-task-type [code system](CodeSystem-specialty-rx-task-type.html) and [value set](ValueSet-specialty-rx-task-type.html)
	- New value in the specialty-rx-task-input-type [code system](CodeSystem-specialty-rx-task-input-type.html) and [value set](ValueSet-specialty-rx-task-input-type.html)
	- New specialty-rx-task-output-type [code system](CodeSystem-specialty-rx-task-output-type.html) and [value set](ValueSet-specialty-rx-task-output-type.html)
- New examples: 
	- [Requested Consent resource (containing a blank consent form)](Consent-specialty-rx-consent-requested-1.html)
	- [Completed Consent resource](Consent-specialty-rx-consent-1.html)
	- [Task illustrating a consent request](Task-specialty-rx-task-consent-request-1.html)
	- [Completed Task after consent is obtained](Task-specialty-rx-task-consent-request-2-completed.html)

<p></p>
<p></p>
<hr>
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
- [Patient Consent Workflows](consent-workflow.html) gives an overview of consent scenarios supported by the guide.
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

### Change Log

<table class="grid">
    <tbody>
        <tr>
                <td>Date</td>
                <td>Change</td>
        </tr>
        <tr>
                <td>Dec 9, 2021</td>
                <td>Initial consent-related updates. Added consent workflow page and profiles for requested consent, completed consent and consent request Task. Initial examples for added profiles.</td>
      	</tr>
        <tr>
                <td>December 20, 2021</td>
                <td>Refined the consent request Task profile (input, output, code elements). Refined the SMART launch Task profile (code and input elements). Added narrative / guidance to the consent request Task and SMART launch Task profile pages. Added specialty-rx-output-type code system and value set for use in the consent request Task profile. Updated the examples. Added an overview of new consent-related content in the Home page.</td>
        </tr>
        <tr>
        	<td>December 31, 2021</td>
                <td>Removed content at the bottom of the Consent Workflows page that duplicated information on the Information Flows Requiring Human Interaction page.</td>
        </tr>
    </tbody> 
</table>
<br />


