### Resource Profiles

These define constraints on FHIR resources that need to be complied with by conformant implementations

<table>
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
<td><a href="StructureDefinition-specialty-rx-bundle-error.html">Specialty Rx Bundle - Error Message</a></td>
<td>This profile constrains a Bundle resource for use as an error message in response to a Specialty Rx Query–with an OperationOutcome resource as the bundle’s message focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-query.html">Specialty Rx Bundle - Query Message</a></td>
<td>This profile constrains a Bundle resource for use as the request message in a Specialty Rx Query process–with a Parameters resource as the bundle’s message focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-query-response.html">Specialty Rx Bundle - Query Response Message</a></td>
<td>This profile constrains a Bundle resource for use as the response message in a Specialty Rx Query process–with a Parameters resource as the bundle’s message focus. </td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html">This profile constrains a Bundle resource for use as the unsolicited query response message in a Specialty Rx Query process–with a Parameters resource as the bundle’s message focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-questionnaire.html">Specialty Rx Bundle - Questionnaire Message</a></td>
<td>This profile constrains a Bundle resource for use as the request message in a Specialty Rx Questionnaire process–with a Parameters resource as the bundle’s message focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-questionnaire-response.html">Specialty Rx Bundle - Questionnaire Response Message</a></td>
<td>This profile constrains a Bundle resource for use as the response message in a Specialty Rx Questionnaire process–with a Parameters resource as the bundle’s message focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-bundle-search-result.html">Specialty Rx Bundle - Search Result</a></td>
<td>This profile constrains a Bundle resource to carry the query results from a Specialty Rx Query.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-condition.html">Specialty Rx Condition</a></td><td>This profile tailors the Condition resource to support specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-coverage.html">Specialty Rx Coverage</a></td>
<td>This profile constrains the Coverage resource for carrying insurance coverage information in the specialty medication prescribing process.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-endpoint-direct.html">Specialty Rx Endpoint - Direct</a></td>
<td>This profile tailors the Endpoint resource to carry a Direct address in specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-medicationrequest.html">Specialty Rx Medication Request</a></td>
<td>This profile tailors the MedicationRequest resource to support specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-query.html">Specialty Rx MessageHeader - Query</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx query data bundle. A Parameters resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-query-response.html">Specialty Rx MessageHeader - Query Response</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx query response bundle. A Parameters resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-error.html">Specialty Rx MessageHeader - Error</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx error bundle. An OperationOutcome resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-query-response-unsolicited.html">Specialty Rx MessageHeader - Query Response - Unsolicited</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx unsolicited query response bundle. A Parameters resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-questionnaire.html">Specialty Rx MessageHeader - Questionnaire</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx questionnaire request bundle. A Parameters resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-messageheader-questionnaire-response.html">Specialty Rx MessageHeader - Questionnaire Response</a></td>
<td>This profile constrains a MessageHeader resource for use in a Specialty Rx questionnaire response bundle. A Parameters resource is the focus.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-organization-payer.html">Specialty Rx Organization - Payer</a></td>
<td>TThis profile tailors the Organization resource to represent a payor organization in the Specialty Medication Prescribing process.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-organization-pharmacy.html">Specialty Rx Organization - Pharmacy</a></td>
<td>Defines further constraints on the US Core Organization resource for use in specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-organization-provider.html">Specialty Rx Organization - Provider</a></td>
<td>This profile tailors the Organization resource to represent a provider organization (clinic, health system, etc.) in the Specialty Medication Prescribing process.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-parameters-query.html">Specialty Rx Parameters - Query</a></td>
<td>This profile tailors the Parameters resource to convey Specialty Rx Query inputs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-parameters-query-response.html">Specialty Rx Parameters - Query Response</a></td>
<td>This profile tailors the Parameters resource to convey Specialty Rx Query outputs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-parameters-questionnaire.html">Specialty Rx Parameters - Questionnaire</a></td>
<td>This profile tailors the Parameters resource to convey Specialty Rx Questionnaire request inputs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-parameters-questionnaire-response.html">Specialty Rx Parameters - Questionnaire Response</a></td>
<td>This profile tailors the Parameters resource to convey Specialty Rx Questionnaire Response inputs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-parameters-query-response-unsolicited.html">Specialty Rx Parameters - Query Response - Unsolicited</a></td>
<td>This profile tailors the Parameters resource to convey Specialty Rx Query Response - Unsolicited content.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-patient.html">Specialty Rx Patient</a></td>
<td>This profile tailors the Patient resource for carrying the patient information needed to support specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-practitioner.html">Specialty Rx Practitioner</a></td>
<td>This profile tailors the Practitioner resource to support specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-practitionerrole.html">Specialty Rx PractitionerRole</a></td>
<td>This profile tailors the Practitioner Role resource to support specialty medication dispensing and enrollment in related programs.</td>
</tr>
<tr>
<td><a href="StructureDefinition-specialty-rx-relatedperson.html">Specialty Rx RelatedPerson</a></td>
<td>This profile tailors the RelatedPerson resource to capture caregivers in the specialty medication dispensing and enrollment in related programs.</td>
</tr>
</tbody>
</table>

<br>

### Message Definitions

These define the types of messages that can be sent and/or received by systems complying with this implementation guide.

<table>
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
<td><a href="MessageDefinition-specialty-rx-error.html">Specialty Rx MessageDefinition - Error</a></td>
<td>Message reporting an error that causes a premature end to processing of a specialty Rx query response message. References the error event.</td>
</tr>
<tr>
<td><a href="MessageDefinition-specialty-rx-query.html">Specialty Rx MessageDefinition - Query</a></td>
<td>Message conveying one or more queries for data related to a prescribed specialty medication. References the query event.</td>
</tr>
    <tr>
<td><a href="MessageDefinition-specialty-rx-query-response.html">Specialty Rx MessageDefinition - Query Response</a></td>
<td>Message conveying the result of one or more queries for data related to a prescribed specialty medication. References the query-response event.</td>
</tr>
   <tr>
<td><a href="MessageDefinition-specialty-rx-query-response-unsolicited.html">Specialty Rx MessageDefinition - Query Response - Unsolicited</a></td>
<td>Unsolicited message conveying data related to a prescribed specialty medication. References the query-response-unsolicited event.</td>
</tr>
   <tr>
<td><a href="MessageDefinition-specialty-rx-questionnaire.html">Specialty Rx MessageDefinition - Questionnaire</a></td>
<td>Message conveying a Questionnaire to obtain information related to a prescribed specialty medication. References the questionnaire event.</td>
</tr>
    <tr>
<td><a href="MessageDefinition-specialty-rx-questionnaire-response.html">Specialty Rx MessageDefinition - Questionnaire Response</a></td>
<td>Message conveying a completed QuestionnaireResponse with information related to a prescribed specialty medication. References the questionnaire-response event.</td>
</tr>
</tbody>
</table>

<br>

### Capability Statements

The following artifacts define the specific capabilities that different types of systems are expected to have in order to comply with this implementation guide. Systems complying with the implementation guide are expected to declare conformance to one or more of the following capability statements.

<table>
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
<td><a href="CapabilityStatement-specialty-rx-data-source.html">Specialty Rx CapabilityStatement - Data Source</a></td>
<td>This CapabilityStatement describes the expected capabilities of a server that is capable of responding to a Specialty Rx Query message posted with the $process-message operation. The server may also support unsolicited delivery of a Specialty Rx Query Response and processing of a Specialty Rx Questionnaire message (returning a Specialty Rx Questionnaire Response message).</td>
</tr>
<tr>
<td><a href="CapabilityStatement-specialty-rx-data-recipient.html">Specialty Rx CapabilityStatement - Data Recipient</a></td>
<td>This CapabilityStatement describes the expected capabilities of a server that is capable of receiving a Specialty Rx Query Response posted with the $process-message operation, and optionally requesting data using the Specialty Rx Query message, requesting completion of questionnaire questions using the Specialty Rx Questionnaire message and receiving completed answers in the Specialty Rx Questionnaire Response message.</td>
</tr>
</tbody>
</table>