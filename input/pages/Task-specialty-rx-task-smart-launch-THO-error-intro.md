<h4>Example notes</h4>

This example uses THO-rooted code system and value set URLs, with the content defined within the IG.

There's an error in this example... it contains a task-type value ("go-out-for-drinks") that isn't in the required task-type value set

<h3>Example data content</h3>

<div class="fm_ex"><span class="emph0">Task</span><br /><span style="display:inline-block"><span class="emph1">id</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">specialty-rx-task-smart-launch-THO-error</span></span></span><br><span style="display:inline-block"><span class="emph1">meta</span><span style="display:inline-block"><span class="emph2">profile</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">http://hl7.org/fhir/us/specialty-rx/StructureDefinition/specialty-rx-task-smart-launch-THO</span></span><br><span style="display:inline-block"><span class="emph1">identifier</span><span style="display:inline-block"><span class="emph2">value</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">launch-context-id-01345005</span></span><br><span style="display:inline-block"><span class="emph1">status</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">requested</span></span></span><br><span style="display:inline-block"><span class="emph1">intent</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">plan</span></span></span><br><span style="display:inline-block"><span class="emph1">code</span><span style="display:inline-block"><span class="emph2">coding</span></span></span><span style="display:inline-block"><span class="emph3">system</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">http://terminology.hl7.org/CodeSystem/task-type</span></span></span><span style="display:inline-block"><span class="emph3">code</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">go-out-for-drinks</span></span></span><span style="display:inline-block"><span class="emph3">display</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="boldValueEmph">Go Out for Drinks (not a value in the value set)</span></span></span><br><span style="display:inline-block"><span class="emph1">description</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">Launch the My Pharmacy SMART app and complete the questionnaire. This contains an invalid task-type value</span></span></span><br><span style="display:inline-block"><span class="emph1">focus</span><span style="display:inline-block"><span class="emph2">identifier</span></span></span><span style="display:inline-block"><span class="emph3">value</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">prescription-70222056</span></span></span><span style="display:inline-block"><span class="emph2">display</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="boldValueEmph">Humira Injector Pen - 9/23/2020</span></span></span><br><span style="display:inline-block"><span class="emph1">for</span><span style="display:inline-block"><span class="emph2">reference</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">Patient/specialty-rx-patient-1</span></span><br><span style="display:inline-block"><span class="emph1">authoredOn</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">2020-09-24</span></span></span><br><span style="display:inline-block"><span class="emph1">requester</span><span style="display:inline-block"><span class="emph2">reference</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">Organization/specialty-rx-organization-pharmacy-1</span></span><span style="display:inline-block"><span class="emph2">display</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="boldValueEmph">Our Pharmacy</span></span></span><br><span style="display:inline-block"><span class="emph1">owner</span><span style="display:inline-block"><span class="emph2">reference</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">Practitioner/specialty-rx-practitioner-1</span></span><span style="display:inline-block"><span class="emph2">display</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="boldValueEmph">Jane Smith MD</span></span></span><br><span style="display:inline-block"><span class="emph1">input</span><span style="display:inline-block"><span class="emph2">type</span></span></span><span style="display:inline-block"><span class="emph3">coding</span><span style="display:inline-block"><span class="emph4">system</span></span></span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">http://terminology.hl7.org/CodeSystem/task-input-type</span></span><span style="display:inline-block"><span class="emph4">code</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">smart-app-launch-url</span></span></span><span style="display:inline-block"><span class="emph4">display</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="boldValueEmph">SMART Application Launch URL</span></span></span><br><span style="display:inline-block"><span class="emph2">valueUrl</span><span style="display:inline-block"><span class="leastEmph fhirValue">@value</span>: &nbsp;<span class="valueEmph">https://my-pharmacy-smart-app.com</span></span></span></div>