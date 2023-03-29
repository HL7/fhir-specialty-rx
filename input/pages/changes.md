### Changes and Updates in STU2
The current official published version of the Specialty Medication Enrollment IG for FHIR R4 is 2.0.0 (STU2). 

This version of the IG adds support for requesting and sharing patient consents and other authorizations that may be needed to fulfill a specialty product prescription. 

Included in this version is the following new content...
<br/>
<ul>
<li><a href="consent-workflow.html">Consent workflows</a> was added to give an overview of consent scenarios supported by the guide</li>
<li><a href="roles.html">Use Cases and Roles</a> was updated to include consent-related scenarios and roles</li>
<li><a href="StructureDefinition-specialty-rx-consent-requested.html">Requested consent profile</a> was added to supply the appropriate form in a consent request</li>
<li><a href="StructureDefinition-specialty-rx-consent.html">Completed consent profile</a> was added to return the completed consents or other authorizations</li>
<li><a href="StructureDefinition-specialty-rx-task-consent-request.html">Consent request task profile</a> was added for requesting consents or other authorizations
<li>Terminology updates:
<ul>
<li>New consent-related value in the <a href="ValueSet-specialty-rx-task-type.html">specialty-rx-task-type value set</a></li>
<li>New consent-related value in the <a href="ValueSet-specialty-rx-task-input-type.html">specialty-rx-task-input-type value set</a></li>
<li>New <a href="ValueSet-specialty-rx-task-output-type.html">specialty-rx-task-output-type value set</a> supporting consent and SMART Lauch tasks</li>
  <li>Combined <a href="CodeSystem-specialty-rx-task-characteristic.html"> specialty-rx-task-characteristic code system</a></li>
</ul>
</li>
<li>New examples: </li>
<ul>
<li><a href="Consent-specialty-rx-consent-requested-1.html">Requested Consent resource (containing a blank consent form)</a></li>
<li><a href="Consent-specialty-rx-consent-1.html">Completed Consent resource</a></li>
<li><a href="Task-specialty-rx-task-consent-request-1.html">Task illustrating a consent request</a></li>
<li><a href="Task-specialty-rx-task-consent-request-2-completed.html">Completed Task after consent is obtained</a></li>
</ul>

