The Coverage elements available to be used by the Specialty Rx process are:

* Coverage.subscriberId: Health plan subscriber ID
* Coverage.subscriber: Subscriber demographic information
* Coverage.identifier: Health plan member ID
* Coverage.beneficiary: Patient demographic information
* Coverage.class=rxid. Pharmacy benefit Member ID
* Coverage.class=rxgroup. Pharmacy benefit Group ID
* Coverage.class=rxbin. Pharmacy benefit BIN (IIN) 
* Coverage.class=rxpcn. Pharmacy benefit PCN 

Different insurers PBMs or other responders may require just a subset of these elements. Implementers may populate all elements for which information is available, or scope the population based the particular responder’s requirements.

### Must Support elements in this profile 
**Client and Responding systems**

The elements identified as Must Support are the typical set used in US pharmacy benefit processing; client systems must enable these to be submitted in requests, and responders must be able to accept them to be used as appropriate during processing.
