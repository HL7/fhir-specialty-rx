### Changes and Updates in STU2
The current official published version of the Specialty Medication Enrollment IG for FHIR R4 is 2.0.0 (STU2). 

This version of the IG adds support for the requesting and sharing of patient consents and other authorizations associated that may be needed to fulfill a specialty product prescription. 

Included in this version is the following new content...
<br/>
<ul>
<li><a href="consent-workflow.html">Consent workflows</a> gives an overview of consent scenarios supported by the guide.</li>
<li><a href="StructureDefinition-specialty-rx-consent-requested.html">Requested consent profile conveying the appropriate blank consent form</a></li>
<li><a href="StructureDefinition-specialty-rx-consent.html">Consent profile for completed specialty consents</a></li>
<li><a href="StructureDefinition-specialty-rx-task-consent-request.html">Task profile used to request consent.</a>. This profile is used in an exchange process based on the FHIR workflow management option <a href="https://www.hl7.org/fhir/workflow-management.html#optiong">POST of Task to fulfiller&#39;s system</a>.</li>
<li>Terminology updates:
<ul>
<li>New value in the specialty-rx-task-type <a href="ValueSet-specialty-rx-task-type.html">value set</a></li>
<li>New value in the specialty-rx-task-input-type <a href="ValueSet-specialty-rx-task-input-type.html">value set</a></li>
<li>New specialty-rx-task-output-type <a href="ValueSet-specialty-rx-task-output-type.html">value set</a></li>
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

