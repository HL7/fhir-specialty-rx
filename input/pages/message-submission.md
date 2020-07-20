### Operation: $process-message
The Specialty Rx Query and Query Response message bundles are pushed to their recipients using the $process-message operation...
* URL: [base]/$process-message

<br>

#### Specialty Rx Query and Query Response: synchronous and asynchronous response

Specialty Rx Query Responses are expected to be systematically produced using data in the patient's electronic health record. They may be returned synchronously or asynchronously in near real-time. 

<br>

#### Specialty Rx Questionnaire and Questionnaire Response: asynchronous response

Specialty Rx Questionnaire Responses are expected to typically depend on human intervention--to be returned asynchronously when complete. 

#### Process-message parameter
The $process-message operation takes a single FHIR resource input parameter consisting of a Bundle containing a MessageHeader resource.  

* In all of the Specialty Rx Query messages the MessageHeader's *focus.reference* points to the Bundle's Parameters resource.

<br>

