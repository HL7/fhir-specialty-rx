### Request / response message flow using CommunicationRequest and Communication

#### Request (Solicited model)

The request for information in the Solicited model is made using a CommunicationRequest resource. The CommunicationRequest identifies:
- the information requested to be exchanged. 

  *The payload.valueString.value holds the query expression and the payload.contentString.value holds the human readable version of that query.*
- the party requesting that the information be exchanged
- the party that is the source of the information to be exchanged
- the party that will receive the information

The CommunicationRequest is sent in a Bundle with related resources that provide context for the request:

- MessageHeader
- MedicationRequest (reflecting the specialty medication prescription)

- Patient (the subject of the MedicationRequest)

- Practitioner (the prescriber of the MedicationRequest)

- Organization representing the dispensing pharmacy

- An additional Organization if the information is to be delivered to party other than the dispensing pharmacy

#### Response or Unsolicited exchange

The responder processes the message payload and collects the data (which could involve manual steps performed by people) and generates a Bundle that contains a Communication resource and the gathered information resources. 

- The responder returns the requested information to the recipient(s) identified in the original CommunicationRequest

- In the Solicited mode, the response is linked to the original request using the identifier that was included in the CommunicationRequest
- The Communication can also contain one or more attachments. 
  
  *The payload.contentAttachment.contentType.value indicates the format for the returned attachments.* *Note: Support for attachments in Specialty Rx is TBD*

- The Communication is sent in a Bundle with related resources:

  - MessageHeader
  - Communication
  - MedicationRequest (reflecting the specialty medication prescription)
  - Patient (the subject of the MedicationRequest)
  - Practitioner (the prescriber of the MedicationRequest)
  - Organization (the dispensing pharmacy)

  *Requested information, such as...*

  - List (referencing requested allergies, conditions, etc.)
  - AllergyIntolerance
  - MedicationStatement
  - Condition
  - Observation
  - Coverage
