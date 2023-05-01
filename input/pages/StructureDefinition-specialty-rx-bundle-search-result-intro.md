The profile reflects typical population of a searchset bundle, ensuring the presence of information the Data Consumer system needs to process the search results.

The profile implements [FHIR searchset response guidance](https://www.hl7.org/fhir/search.html#conformance) that allows the Data Consumer to be confident about what search parameters were used as criteria when processing the request. The Data Source system SHALL populate `Bundle.link.relation` with "self" and `Bundle.link.url` with the parameters that were actually used to process the search. For example:

```
"link" : [
  {
   "relation" : "self",
   "url" : "Coverage?patient=patientEHR"
  }
]
```
<br/>

**Examples.** This profile is illustrated in the following full message examples:
- [Specialty Rx Query Response 1](Bundle-specialty-rx-query-response-1.html)
- [Specialty Rx Query Response 2](Bundle-specialty-rx-query-response-2.html)
- [Specialty Rx Query Response 3 with operation outcome](Bundle-specialty-rx-query-response-3-w-op-outcome.html)
- [Specialty Rx Query Response Unsolicited 1](Bundle-specialty-rx-query-response-unsolicited-1.html)

<p></p>
