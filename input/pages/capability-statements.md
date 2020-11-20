This guide offers multiple implementation options to fit differing participant goals, preferences and trading partner capabilities. The Capability Statements below each define a set of functionality that may be implemented alone or in combination.

The RESTful options enable participants with the ability to establish direct endpoint connections to fulfill the guide's use cases with standard FHIR RESTful capabilities. 

Implementers that wish to leverage an existing messaging arrangement can meet the use cases using the FHIR messaging option. For example, a pharmacy that performs prescription workflows through an exchange network--and doesn't have access to trading partners' endpoint details, patient resource identifiers, etc.--can leverage the messaging option's mechanisms for routing and patient matching that fit that environment.

<h3>Data Source Capability Statements</h3>

A Data Source System SHALL conform to at least one of the following Capability Statements, and MAY conform to both:
- [Specialty Rx Data Source - RESTful](CapabilityStatement-specialty-rx-data-source-restful.html)
- [Specialty Rx Data Source - Messaging](CapabilityStatement-specialty-rx-data-source-messaging.html)

<h3>Requesting System Capability Statements</h3>
A Requesting System SHALL conform to at least one of the following Capability Statements, and MAY conform to both:
- [Specialty Rx Requesting System - RESTful](CapabilityStatement-specialty-rx-data-recipient-restful.html)
- [Specialty Rx Requesting System - Messaging](CapabilityStatement-specialty-rx-data-recipient-messaging.html)



<br>



