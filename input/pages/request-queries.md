### Specifying a query string

The Specialty Rx data request specifies the desired patient information in the payload element of a CommunicationRequest resource. 

The process utilizes the *cdex-payload-query-string* extension (defined in the Da Vinci Clinical Data Exchange (CDex) Implementation Guide) to specify each query using standard FHIR search parameters. The query string is conveyed in the extension's valueString element.

**Example:** Excerpt from CommunicationRequest

```
 "payload" : [
    {
      "extension" : [
        {
          "url" : "http://hl7.org/fhir/us/davinci-cdex/StructureDefinition/cdex-payload-query-string",
          "valueString" : "Condition?patient=specialty-rx-patient-1"
        }
      ],
      "contentString" : "Please provide the patient's conditions"
    }
```

<br>

### Required query strings

To ensure that the most common data requests are supported by all participants, responders MUST be able to respond to the following query strings:

| Query String                                                 | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Condition?patient=[patient ref]                              | All patient conditions                                       |
| AllergyIntolerance?patient=[patient ref]                     | All patient allergies and intolerances                       |
| Observation?patient=[patient ref]&category=vital-signs&date=[date period range] | All patient vital signs recorded in the specified date period |
| Coverage?patient=[patient ref]                               | All patient insurance coverage                               |
| MedicationStatement?patient=[patient ref]                    | All patient medications                                      |

<br>

### Optional query strings

Responders SHOULD support the following queries, which make up the standard set of requests used in the Specialty Rx process:

| Query String                                               | Description                                                  |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| Observation?patient=[patient ref]&date=[date period range] | All patient observations recorded during the specified date period |
| *others TBD*                                               |                                                              |

<br>

<br>

