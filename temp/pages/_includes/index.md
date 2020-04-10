### Overview
This FHIR implementation Guide describes the exchange of data (demographic, prescription, clinical and financial) for dispensing specialty medications by pharmacies as well as facilitating enrollment of patients in programs offered by third parties such as but not limited to Hub vendors and Pharmaceutical manufacturers.

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

  <table>
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
  <table>
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
		<td>Additional content: profiles and examples for PractitionerRole, Endpoint, Organization, Location, Endpoint</td>
  	  </tr>
	</tbody>
  </table>