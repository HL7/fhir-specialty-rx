### US Core Search Guidance

Data Source and Data Consumer systems SHALL follow US Core search requirements and guidance when performing searches associated with this guide.

### Required Searches

To ensure that the most common data requests are supported by all participants, Data Sources SHALL be able to return information in response to searches on the resources below--whether responding to RESTful search requests or the Specialty Rx Query message. 

*Note: When specifying searches in the Specialty Rx Query message, the patient parameter is omitted (see [below](#search-conventions-in-the-specialty-rx-query-message))*
														        
<table class="grid">
<thead>
<tr>
<th>Resource</th>
<th style="min-width:200px">Parameters</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>AllergyIntolerance</td>
    <td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-allergyintolerance.html#mandatory-search-parameters">Per US Core</a></td>
    <td><pre>AllergyIntolerance?patient=123&amp;clinical-status=active</pre>Returns all active patient allergies and intolerances
    </td>
</tr>
<tr>
<td>Condition</td>
    <td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-condition.html#mandatory-search-parameters">Per US Core</a></td>
<td><pre>Condition?patient=123</pre>Returns all patient conditions</td>
</tr>
<tr>
<td>Observation</td>
    <td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-observation-lab.html#mandatory-search-parameters">Per US Core</a></td>
    <td><pre>Observation?patient=123&amp;category=vital-signs&amp;date=ge2020-01-01</pre>Returns all patient vital signs recorded in the specified date period</td>
</tr>
<tr>
<td>Coverage</td>
    <td>SHALL: patient<br/>SHOULD: beneficiary<br/><span style="font-size:smallest; font-style:italic">(Not profiled in US Core)</span></td>
<td><pre>Coverage?patient=123</pre>Returns all patient insurance coverages</td>
</tr>
<tr>
<td>MedicationRequest</td>
    <td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-medicationrequest.html#mandatory-search-parameters">Per US Core</a></td>
<td><pre>MedicationRequest?patient=123&amp;intent=order&amp;status=active&amp;_include=MedicationRequest:Medication</pre>Returns all active patient MedicationRequest orders and the associated Medications</td>
</tr>
</tbody>
</table>


<p></p>

### Recommended Searches

In addition to the required searches above, implementers SHOULD support DocumentReference searches and retrieval, to enable those participating in the fulfillment of specialty medication prescriptions to access patient information recorded in patient documents.

<table class="grid">
<thead>
<tr>
<th>Resource</th>
<th style="width:200px">Parameters</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
    <td>DocumentReference</td>
    <td><a href="https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-documentreference.html#mandatory-search-parameters">See US Core</a></td>
<td><pre>DocumentReference?patient=123 &amp;category=http://hl7.org/fhir/us/core/CodeSystem/us-core-documentreference-category|clinical-note</pre>Returns all patient clinical notes</td>
</tr>
</tbody>
</table>
<p></p>

<p></p>

### Optional Searches

Data Consumers MAY include searches other than those outlined above. 

- Data Source systems SHALL return a [search-result](StructureDefinition-specialty-rx-bundle-search-result.html) for each--even if the search is not supported--which SHALL include an OperationOutcome indicating when the Data Source does not support the submitted search or search parameter.  

<p></p>
### Returning related resources within search results

Data Sources SHALL be capable of supporting the `_revinclude=Provenance:target` parameter as defined in US Core, returning [US Core Provenance](https://www.hl7.org/fhir/us/core/StructureDefinition-us-core-provenance.html) resource(s) that reference returned resources, as specified [here in US Core](https://www.hl7.org/fhir/us/core/CapabilityStatement-us-core-server.html). In addition, Data Sources SHALL support mandatory `_include` parameters defined in US Core.

Each related resource SHALL be included as an entry in the response's searchset bundle with a `search.mode` value of `include`. Below are examples:

- [`_include` : MedicationRequest referencing an included Medication resource](Bundle-specialty-rx-search-response-1-w-include.html)
- [`_revinclude` : AllergyIntolerance with an included Provenance resource](Bundle-specialty-rx-search-response-2-w-revinclude.html)

<p></p>

### Further search guidance

This guide leverages search guidance given in the US Core FHIR Implementation Guide and the base FHIR specification. 

- [US Core Search syntax](https://www.hl7.org/fhir/us/core/general-guidance.html#search-syntax)

- [FHIR Search guidance](http://hl7.org/fhir/R4/search.html)

<p></p>
### Search conventions in the Specialty Rx Query Message

The Specialty Rx Query message requests specific information from a given patient's records in the responding system. The desired information is specified as FHIR search statements which are sent as parameters in the message. Responders are expected to execute these searches for the patient supplied in the request and return the results in a Specialty Rx Query Response message.

#### Specifying a query string

Specialty Rx messaging enables Data Consumer systems to submit requests without performing a patient match ahead of time. This accommodates a common situation where the Data Consumer hasn't participated in previous FHIR exchanges about this patient with the Data Source and doesn't possess the Data Source's Patient resource ID. This also addresses challenges that may arise if the Data Consumer interacts with the Data Source via an intermediary--for example if the Data Consumer lacks details about the Data Source's endpoint or is otherwise unable to submit patient match requests directly to the Data Source.

To support this scenario, the Specialty Rx Query message omits the patient parameter from submitted search strings, with the expectation that the Data Source will append it after locating the desired patient in its system.  

For example, a search for a given patient's vital signs that would ordinarily be stated as:

`Observation?patient=[patient id]&category=vital-signs`

... is submitted in the Specialty Rx Query without the patient search parameter:

`Observation?category=vital-signs`

#### Identifying the desired patient

The Data Consumer identifies the desired patient by including one or both the following in the Specialty Rx Query message:

- a Patient resource representing the patient in the Data Consumer system (mandatory)
- a Patient resource from the Data Source system (if available)

The Data Source locates the desired patient and completes the query string as follows, based on the submitted patient information:

- If the **request includes only the Data Consumer's Patient**, the Data Source performs a matching process and locates the associated patient in its own system. It appends its Patient ID to each submitted search string.
- If the **request includes both the Data Consumer's Patient and Data Source's Patient**, the Data Source confirms the match and then appends its Patient ID to each submitted search string. 

#### Returning the executed search string in the response message

In the Specialty Rx Query Response, the Data Source returns the full search string that was ultimately executed--including patient parameter--in the .link element of each returned searchset Bundle.

<pre>
Bundle
    .link
        .relation = "self"
        .url = "MedicationRequest?patient=12345&status=active"
    .entry
</pre>
#### Patient references within search results

All searches performed within a request/response exchange flow relate to a single patient, who is represented in the *responder-patient* parameter in the Query Response message bundle. Patient references contained in resources in searchset bundles SHOULD be resolvable to the *responder-patient* entry in the outer, Query Response message bundle.

<br />

