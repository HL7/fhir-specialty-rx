### Operation: $process-message
The Specialty Rx request and response message bundles are pushed to their recipients using the $process-message operation...
* URL: [base]/$process-message

<br>

#### Asynchronous response

Specialty Rx responses are returned asynchronously. Responses that can be systematically produced using data in the patient's electronic health record are expected to be returned in near real-time. In some cases, responses may depend on human intervention--to be returned when complete. 

#### Process-message parameter
The $process-message operation takes a single FHIR resource input parameter consisting of a Bundle containing a MessageHeader resource.  

* In the Specialty Rx Request, the MessageHeader's *focus.reference* points to the Bundle's CommunicationRequest resource, per the SpecialtyRxRequestMessageDefinition.
* In the response, the *focus.reference* points to the Bundle's Communication resource, per the SpecialtyRxResponseMessageDefinition.

<br>

<a href="Bundle-specialty-rx-request-bundle-1.html">Example bundled Specialty Rx data request</a>

<a href="Bundle-specialty-rx-response-bundle-1.html">Example bundled Specialty Rx data response</a>

<br><br>

