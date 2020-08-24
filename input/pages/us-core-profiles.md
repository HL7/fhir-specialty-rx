### US Core Profiles Used in this Guide

Specialty medication fulfillment involves information in addition to what is reflected in the resource profiles defined in this implementation guide. 

Stakeholders reviewed the following US Core profiles and found that they met the needs of the Specialty Rx process without further constraints. Implementers are expected to use these profiles when exchanging the related resources during the Specialty Rx process.

<table class="grid" style="width:100%">
<colgroup>
  <col width="300">
  <col>
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-allergyintolerance.html">US Core AllergyIntolerance Profile</a></td>
<td>This profile sets minimum expectations for the AllergyIntolerance resource to record, search, and fetch allergies/adverse reactions associated with a patient.</td>
</tr>
<tr>
<td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-careteam.html">US Core CareTeam Profile</a></td>
<td>This profile sets minimum expectations for the CareTeam resource for identifying the Care Team members associated with a patient.</td>
</tr>
<tr>
<td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-observation-lab.html">US Core Laboratory Result Observation Profile</a></td>
<td>This profile sets minimum expectations for the Observation resource resource to record, search, and fetch laboratory test results associated with a patient.</td>
</tr>
<tr>
<td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-location.html">US Core Location Profile</a></td>
<td>This profile sets minimum expectations for the Location resource for recording, searching for and fetching a Location associated with a patient, provider or organization.</td>
</tr>
</tbody>
</table>

<br>

Further, when other resources not profiled in this implementation guide or in the list above are exchanged as part of a Specialty Rx workflow (e.g., returned in response to a Specialty Rx Query message), they are expected to conform to the associated US Core profile if one exists.

<br>

