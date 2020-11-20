<h3>FHIR RESTful Capabilities</h3>
Specialty Rx Data Recipient **SHALL**: 
1. Support the Unsolicited workflow defined in this Guide and respond to the $process-message operation carrying a Specialty Rx Query Response - Unsolicited. 
1. Support the json source format. 
1. Declare a CapabilityStatement identifying the profiles supported.

Specialty Rx Data Recipient **SHOULD**: 
1. Support the xml source format. 
1. Identify the Specialty Rx profiles supported as part of the FHIR `meta.profile` attribute for each applicable instance. 

The Specialty Rx Data Recipient MAY 
1. Support the Solicited workflow defined in this Guide, including the Specialty Rx Query, Specialty Rx Query Response, and Specialty Rx Error messages. 
1. Support the Patient/$match operation.

<h3>Security</h3>
1. For general security considerations refer to [FHIR Security and Privacy Considerations](http://build.fhir.org/secpriv-module.html). 
1. For additional security guidance, refer to the [core FHIR Security guidance page](https://www.hl7.org/fhir/security.html). 
1. A server **SHALL** reject any unauthorized requests by returning an `HTTP 401` unauthorized response code.

<br/>