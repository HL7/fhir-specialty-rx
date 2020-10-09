### Operation: $process-message
All Specialty Rx messages are submitted to their recipients using the $process-message operation...
* URL: [base]/$process-message

<br>

### Synchronous or asynchronous response

**Specialty Rx Query Responses** are expected to be systematically produced using data in the patient's electronic health record. They may be returned synchronously or asynchronously in near real-time. The *requesting system* cannot influence which behavior occurs; when a message is received, the *data source* determines whether it will respond synchronously or asynchronously.

**Specialty Rx Questionnaire Responses** will typically require human intervention--to be returned asynchronously when complete. 

<br/>

### Process-message parameter
The $process-message operation takes a single FHIR resource input parameter consisting of a Bundle containing a MessageHeader resource.  

* In all of the Specialty Rx messages, the MessageHeader's *focus.reference* points to the message Bundle's Parameters resource.

<br>

