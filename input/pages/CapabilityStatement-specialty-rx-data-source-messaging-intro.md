<h3>FHIR RESTful Capabilities</h3>
Specialty Rx Data Source **SHALL**: 
1. Support the Solicited workflow defined in this guide by responding to the $process-message operation containing a Specialty Rx Query message by returning a Specialty Rx Query Response message or Specialty Rx Error message. 
1. Support all required RESTful searches and search parameters. 
1. Support the JSON source format. 
1. Declare a CapabilityStatement identifying the profiles supported.
1. Follow US Core search requirements and guidance when performing searches associated with this IG.

Specialty Rx Data Source **SHOULD**: 
1. Respond to the Patient/$match operation.  
1. Support the XML source format. 
1. Identify the Specialty Rx profiles supported as part of the FHIR `meta.profile` attribute for each applicable instance.

The Specialty Rx Data Source MAY 
1. Support the Unsolicited workflow defined in this guide, using the Specialty Rx Query Response - Unsolicited message. 
1. Support the Task / SMART application launch capability specified in the guide.
1. Support the Task / Consent Request capability specified in the guide.

<h3>Security</h3>

1. For general security considerations refer to [FHIR Security and Privacy Considerations](https://www.hl7.org/fhir/secpriv-module.html).
2. For additional security guidance, refer to the [core FHIR Security guidance page](https://www.hl7.org/fhir/security.html).
3. A server **SHALL** reject any unauthorized requests by returning an `HTTP 401` unauthorized response code.

### Resources

- AllergyIntolerance, Condition, Coverage, DocumentReference, MedicationRequest and Observation actions referenced below are executed in the context of message processing. 

- Task interactions referenced below are RESTful. 

- OperationOutcome interactions referenced below are within both messaging and RESTful actions.

<table class="grid">
	<tbody>
		<tr>
			<th>
				<b></b>
			</th>
			<th>
				<b>Resource Type</b>
			</th>
			<th>
				<b>Profile</b>
			</th>
			<th>
				<b title="GET a resource (read interaction)">Read</b>
			</th>
			<th>
				<b title="GET all set of resources of the type (search interaction)">Search</b>
			</th>
			<th>
				<b title="PUT a new resource version (update interaction)">Update</b>
			</th>
			<th>
				<b title="POST a new resource (create interaction)">Create</b>
			</th>
		</tr>
		<tr>
			<td>SHALL</td>
            <td>AllergyIntolerance</td>
			<td>
				<a href="http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance">http://hl7.org/fhir/us/core/StructureDefinition/us-core-allergyintolerance</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Condition</td>
			<td>
				<a href="http://hl7.org/fhir/us/core/StructureDefinition/us-core-condition">http://hl7.org/fhir/us/core/StructureDefinition/us-core-condition</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Coverage</td>
			<td>
				<a href="http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-coverage">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-coverage</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHOULD</td>
			<td>DocumentReference</td>
			<td>
				<a href="http://hlhttp://hl7.org/fhir/us/core/StructureDefinition/us-core-documentreference">http://hl7.org/fhir/us/core/StructureDefinition/us-core-documentreference</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>MedicationRequest</td>
			<td>
				Search results: <br /><a href="http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest">http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest</a>
                <br /><br />Identifying the prescribed medication in messaging: <br /><a href="StructureDefinition-specialty-rx-medicationrequest.html">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-medicationrequest.html</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Observation</td>
			<td>
				<a href="http://hl7.org/fhir/us/core/StructureDefinition/us-core-observation-lab">http://hl7.org/fhir/us/core/StructureDefinition/us-core-observation-lab</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>OperationOutcome</td>
			<td>
				<a href="http://hl7.org/fhir/StructureDefinition/OperationOutcome">http://hl7.org/fhir/StructureDefinition/OperationOutcome</a>
			</td>
			<td>y</td>
			<td></td>
			<td></td>
			<td>y</td>
		</tr>
		<tr>
			<td>MAY</td>
			<td>Task</td>
			<td>
				<a href="http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-task-smart-launch">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-task-smart-launch</a>
			</td>
			<td>y</td>
			<td></td>
			<td>y</td>
			<td>y</td>
		</tr>
				<tr>
			<td>MAY</td>
			<td>Task</td>
			<td>
				<a href="http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-task-consent-request">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-task-consent-request</a>
			</td>
			<td>y</td>
			<td></td>
			<td>y</td>
			<td>y</td>
		</tr>
		<tr>
			<td>MAY</td>
			<td>Consent</td>
			<td>
				<a href="http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-consent">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-consent</a>
			</td>
			<td>y</td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>MAY</td>
			<td>Consent</td>
			<td>
				<a href="http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-consent-requested">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-consent-requested</a>
			</td>
			<td>y</td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>
<h3>Search</h3>

Data Source systems SHALL follow US Core search requirements and guidance when performing searches associated with this guide. See the [Search Conventions](searches.html) section.

### Messaging

<table class="grid">
	<tbody>
		<tr>
			<th>
				<b></b>
			</th>
			<th>
				<b>Mode</b>
			</th>
			<th>
				<b>Message Type</b>
			</th>
			<th>
				<b>Message Definition</b>
			</th>
			<th>
				<b>Message Bundle</b>
			</th>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Receiver</td>
            <td>Specialty Rx Query</td>
			<td>
				<a href="MessageDefinition-specialty-rx-query.html">http://hl7.org/fhir/us/specialty-rx/MessageDefinition/specialty-rx-query</a>				
			</td>
			<td>
            <a href="StructureDefinition-specialty-rx-bundle-query.html">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-bundle-query</a>                
            </td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Sender</td>
            <td>Specialty Rx Query Response</td>
			<td>
				<a href="MessageDefinition-specialty-rx-query-response.html">http://hl7.org/fhir/us/specialty-rx/MessageDefinition/specialty-rx-query-response</a>
			</td>
			<td>
            <a href="StructureDefinition-specialty-rx-bundle-query-response.html">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-bundle-query-response</a>                
            </td>
		</tr>
		<tr>
			<td>SHALL</td>
			<td>Receiver and Sender</td>
            <td>Specialty Rx Error</td>
			<td>
				<a href="MessageDefinition-specialty-rx-error.html">http://hl7.org/fhir/us/specialty-rx/MessageDefinition/specialty-rx-error</a>
			</td>
			<td>
            <a href="StructureDefinition-specialty-rx-bundle-error.html">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-bundle-error</a>                
            </td>
		</tr>
		<tr>
			<td>MAY</td>
			<td>Sender</td>
            <td>Specialty Rx Query Response - Unsolicited</td>
			<td>
				<a href="MessageDefinition-specialty-rx-query-response-unsolicited.html">http://hl7.org/fhir/us/specialty-rx/MessageDefinition/specialty-rx-query-response-unsolicited</a>
			</td>
			<td>
            <a href="StructureDefinition-specialty-rx-bundle-query-response-unsolicited.html">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-bundle-query-response-unsolicited</a>                
            </td>
		</tr>
	</tbody>
</table>

<br />