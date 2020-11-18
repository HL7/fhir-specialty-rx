### Query Request Message

The Query message requests information from a patient's health records. It identifies the patient and specifies searches to be performed on the responding system's server.

It is a message Bundle with: 

- an event type equal to `query`
- a Parameters resource as the `focus` (see below)
  - Search strings are specified in `query-string` parameter elements 
- a mandatory Patient resource representing the requesting party's understanding of the patient
- an optional Patient representing the patient in the responder's system
- optional MedicationRequest, Practitioner, Organization resources to represent the associated specialty prescription

*See [Processing Detail](patient-matching.html) for patient matching and other processing expectations.*

<table class="grid">
<thead>
<tr>
<th>Parameter</th>
<th>Cardinality</th>
<th>Type</th>
<th>Description, profile</th>
</tr>
</thead>
<tbody>
<tr>
<td>query-string</td>
<td>1..*</td>
<td>string</td>
<td>Search string. See <a href="request-queries.html">Search Conventions</a></td>
</tr>
<tr>
<td>requester-patient</td>
<td>1..1</td>
<td>Patient</td>
<td>Patient resource representing the requesting party&#39;s understanding of the patient<br /><em>Profile: <a href="StructureDefinition-specialty-rx-patient.html">specialty-rx-patient</a></em></td>
</tr>
<tr>
<td>responder-patient</td>
<td>0..1</td>
<td>Patient</td>
<td>Patient resource representing the responding party&#39;s understanding of the patient, if available<br /><em>Profile: <a href="StructureDefinition-specialty-rx-patient.html">specialty-rx-patient</a></em></td>
</tr>
<tr>
<td>medication-request</td>
<td>0..1</td>
<td>MedicationRequest</td>
<td>The associated specialty prescription, which may be included to assist patient matching<br /><em>Profile: <a href="StructureDefinition-specialty-rx-medicationrequest.html">specialty-rx-medicationrequest</a></em></td>
</tr>
<tr>
<td>prescriber</td>
<td>0..1</td>
<td>Practitioner</td>
<td>The prescriber of the associated specialty prescription<br /><em>Profile: <a href="StructureDefinition-specialty-rx-practitioner.html">specialty-rx-practitioner</a></em></td>
</tr>
<tr>
<td>pharmacy</td>
<td>0..1</td>
<td>Organization</td>
<td>The pharmacy dispensing the associated specialty prescription<br /><em>Profile: <a href="StructureDefinition-specialty-rx-organization-pharmacy.html">specialty-rx-organization-pharmacy</a></em></td>
</tr>
</tbody>
</table>



<br />	

### Query Response Message

The Query Response message returns the requested information from a patient's health records. 

It is a message Bundle with: 

- an event type equal to 'query-response'
- a Parameters resource as the focus (see below)
- a mandatory Patient resource representing the requesting party's understanding of the patient
- a mandatory Patient representing the patient in the responder's system
- Searchset bundle(s) containing search results

*See [Processing Detail](patient-matching.html) for patient matching and other processing expectations.*

<table class="grid">
<thead>
<tr>
<th>Parameter</th>
<th>Cardinality</th>
<th>Type</th>
<th>Description, profile</th>
</tr>
</thead>
<tbody>
<tr>
<td>requester-patient</td>
<td>1..1</td>
<td>Patient</td>
<td>Patient resource representing the requesting party&#39;s understanding of the patient<br /><em>Profile: <a href="StructureDefinition-specialty-rx-patient.html">specialty-rx-patient</a></em></td>
</tr>
<tr>
<td>responder-patient</td>
<td>1..1</td>
<td>Patient</td>
<td>Patient resource representing the responding party&#39;s understanding of the patient<br /><em>Profile: <a href="StructureDefinition-specialty-rx-patient.html">specialty-rx-patient</a></em></td>
</tr>
<tr>
<td>search-result</td>
<td>1..*</td>
<td>Bundle</td>
<td>Searchset bundle containing the results from a single search contained in the request<br />*Profile: <a href="StructureDefinition-specialty-rx-bundle-search-result.html">specialty-rx-bundle-search-result</a></td>
</tr>
</tbody>
</table>
<br />

### Query Response - Unsolicited Message

The Query Response - Unsolicited message transmits information from a patient's health record to a stakeholder involved in fulfillment of a specialty medication. This message is not preceded by a request but instead is by a process event--typically sent when the medication is prescribed.

It is a message Bundle with: 

- an event type equal to 'query-response-unsolicited'
- a Parameters resource as the focus (see below)
- a mandatory Patient representing the patient in the sender's system
- mandatory MedicationRequest, Practitioner, Organization resources to represent the associated specialty prescription
- Searchset bundle(s) containing patient data captured as search results

*See [Processing Detail](patient-matching.html) for patient matching and other processing expectations.*

<table class="grid">
<thead>
<tr>
<th>Parameter</th>
<th>Cardinality</th>
<th>Type</th>
<th>Description, profile</th>
</tr>
</thead>
<tbody>
<tr>
<td>source-patient</td>
<td>1..1</td>
<td>Patient</td>
<td>Patient resource representing the data source&#39;s understanding of the patient<br /><em>Profile: <a href="StructureDefinition-specialty-rx-patient.html">specialty-rx-patient</a></em></td>
</tr>
<tr>
<td>medication-request</td>
<td>1..1</td>
<td>MedicationRequest</td>
<td>The associated specialty prescription<br /><em>Profile: <a href="StructureDefinition-specialty-rx-medicationrequest.html">specialty-rx-medicationrequest</a></em></td>
</tr>
<tr>
<td>prescriber</td>
<td>1..1</td>
<td>Practitioner</td>
<td>The prescriber of the associated specialty prescription<br /><em>Profile: <a href="StructureDefinition-specialty-rx-practitioner.html">specialty-rx-practitioner</a></em></td>
</tr>
<tr>
<td>pharmacy</td>
<td>1..1</td>
<td>Organization</td>
<td>The pharmacy dispensing the associated specialty prescription<br /><em>Profile: <a href="StructureDefinition-specialty-rx-organization-pharmacy.html">specialty-rx-organization-pharmacy</a></em></td>
</tr>
<tr>
<td>search-result</td>
<td>1..*</td>
<td>Bundle</td>
<td>Searchset bundle containing the results from a single search of patient data<br />*Profile: <a href="StructureDefinition-specialty-rx-bundle-search-result.html">specialty-rx-bundle-search-result</a></td>
</tr>
</tbody>
</table>

<br>

