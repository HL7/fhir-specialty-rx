### Data request queries

The Specialty Rx Query message requests specific information from a patient's records in the responding system. The desired information is specified as FHIR search statements in parameters contained in the request. Responders are expected to execute these searches for the patient supplied in the request and return the results in a Specialty Rx Query Response message.

#### Specifying a query string

Specialty Rx messaging enables requesters to submit requests without performing a patient match ahead of time. This accommodates the typical situation where the requester hasn't participated in previous FHIR exchanges with the responder and so doesn't possess the responder's patient resource. This  is accomplished by omitting the patient parameter from submitted search strings.

For example, a search for a given patient's vital signs might typically be stated as:

- *Observation?patient=[patient id]&category=vital-signs&date=[date period range]*

In the Specialty Rx Query, the patient search parameter is omitted, with the expectation that the responder will append it after locating the desired patient in its system:

- *Observation?category=vital-signs&date=[date period range]*

In the Specialty Rx Query Response, the responder returns the full search string, including patient parameter, in the Bundle.entry.link element of the response Bundle containing each List of search results.

*Bundle*

​     *.entry*

​        *.link.relation = "self"*

​        *.link.url = "Observation&patient=340520450&category=vital-signs&date=ge2019-01-01"*

​        *.fullUrl = [list URL]*

​        *.resource.List = [the List resource containing the resulting set of Observations]*

 

### Required query strings

To ensure that the most common data requests are supported by all participants, responders MUST be able to respond to the following query strings:

| Query String                                              | Description                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| Condition                                                 | All patient conditions                                       |
| AllergyIntolerance                                        | All patient allergies and intolerances                       |
| Observation?category=vital-signs&date=[date period range] | All patient vital signs recorded in the specified date period |
| Coverage                                                  | All patient insurance coverage                               |
| MedicationStatement                                       | All patient medications                                      |

<br>

### Optional query strings

Responders SHOULD support the following queries, which make up the standard set of requests used in the Specialty Rx process:

| Query String                         | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| Observation?date=[date period range] | All patient observations recorded during the specified date period |
| *others TBD*                         |                                                              |

<br>

<br>

