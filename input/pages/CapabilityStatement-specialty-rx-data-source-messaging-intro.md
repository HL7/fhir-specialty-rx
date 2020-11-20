<h3>FHIR RESTful Capabilities</h3>
Specialty Rx Data Source **SHALL**: 
1. Support the Solicited workflow defined in this guide by responding to the $process-message operation containing a Specialty Rx Query message by returning a Specialty Rx Query Response message or Specialty Rx Error message. 
1. Support all required RESTful searches and search parameters. 
1. Support the json source format. 
1. Declare a CapabilityStatement identifying the profiles supported.

Specialty Rx Data Source **SHOULD**: 
1. Respond to the Patient/$match operation.  
1. Support the xml source format. 
1. Identify the Specialty Rx profiles supported as part of the FHIR `meta.profile` attribute for each applicable instance.

The Specialty Rx Data Source MAY 
1. Support the Unsolicited workflow defined in this guide, using the Specialty Rx Query Response - Unsolicited message. 
1. Support the Task / SMART application launch capability specified in the guide.

<h3>Security</h3>
1. For general security considerations refer to [FHIR Security and Privacy Considerations](http://build.fhir.org/secpriv-module.html). 
1. For additional security guidance, refer to the [core FHIR Security guidance page](https://www.hl7.org/fhir/security.html). 
1. A server **SHALL** reject any unauthorized requests by returning an `HTTP 401` unauthorized response code.

<br/>