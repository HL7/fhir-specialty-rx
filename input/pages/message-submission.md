### Operation: $process-message
Specialty Rx messages are POSTed to their recipients using the $process-message operation...
* URL: [base]/$process-message

Details from the base FHIR specification are [here](https://www.hl7.org/fhir/operation-messageheader-process-message.html).

<br>

### $process-message Parameters
The $process-message operation SHALL contain a single `content` parameter consisting of a FHIR message (a Bundle containing a MessageHeader resource).  

**Notes:** 

- Because the Process Message operation does not use the Parameters resource, the "content" parameter is always the body of the HTTP message.

- The `async` and `response-url` Process Message parameters are not to be used when exchanging Specialty Rx messages.

<br>

### Synchronous or Asynchronous Response

Specialty Rx Query Responses are expected to be systematically produced using data in the patient's electronic health record. They may be returned synchronously or asynchronously in near real-time. The Requesting System cannot influence which behavior occurs; when a message is received, the Data Source System determines whether it will respond synchronously or asynchronously.

- When responding asynchronously, the Data Source System first acknowledges the request message with a `200 OK` with no body, or returns an HTTP error if the message cannot be processed

<br/>

### Error Response

See [Error Handling](error-handling.html) for instances where the request cannot be processed in part or in whole.

<br>