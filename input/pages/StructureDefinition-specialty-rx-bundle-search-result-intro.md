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

