<h3>FHIR RESTful Capabilities</h3>
Specialty Rx Data Consumer **SHALL**: 
1. Support the RESTful solicited workflow defined in this guide, including all required searches and search parameters. 
1. Implement the RESTful behavior according to the FHIR specification. 
1. Support the JSON source format. 
1. Declare a CapabilityStatement identifying the profiles supported.

Specialty Rx Data Consumer **SHOULD**: 
1. Support the Patient/$match operation. 
1. Support the recommended searches and parameters identified in the guide. 
1. Identify the Specialty Rx profiles supported as part of the FHIR `meta.profile` attribute for each applicable instance.

The Specialty Rx Data Consumer MAY 
1. Support the Task / SMART application launch capability specified in the guide.

<h3>Security</h3>
1. For general security considerations refer to [FHIR Security and Privacy Considerations](https://www.hl7.org/fhir/secpriv-module.html). 
1. For additional security guidance, refer to the [core FHIR Security guidance page](https://www.hl7.org/fhir/security.html). 

### Resources

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
			<td>SHOULD</td>
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
			<td>SHOULD</td>
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
			<td>SHOULD</td>
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
			<td>SHOULD</td>
			<td>MedicationRequest</td>
			<td>
				<a href="http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest">http://hl7.org/fhir/us/core/StructureDefinition/us-core-medicationrequest</a>
			</td>
			<td>y</td>
			<td>y</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td>SHOULD</td>
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
	</tbody>
</table>
<h3>Search</h3>

Data Consumer systems SHALL follow US Core search requirements and guidance when performing searches associated with this guide. See the [Search Conventions](searches.html) section.

<br />

