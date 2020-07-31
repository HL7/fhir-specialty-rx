### Failure or non-execution of an individual search within a Query

If a data source system...

- is unable to execute an individual search included in a Query message

  or 

- encounters a non-fatal exception when executing an individual search 

the system SHALL include a searchset Bundle containing the search string and an OperationOutcome describing the issue as a *query-result* parameter in the Query Response message. 

[Example](Bundle-specialty-rx-query-response-3-w-op-outcome.html)

<br/>

### Error preventing the return of a Query Response

When a data source system encounters an error that prevents it from responding to a Query message with a Query Response, it  SHALL respond by returning a Query Response Error message containing an OperationOutcome resource that describes the nature of the failure.

The OperationOutcome:

* SHALL contain a definition of severity in the OperationOutcome.issue.severity field. 
* SHALL contain a definition of the type of error in the OperationOutcome.issue.code element.
* SHOULD provide additional diagnostic details of the error in OperationOutcome.diagnostics property
* SHOULD contain details of the error in the OperationOutcome.issue.details.coding.display field.
* SHOULD contain an OperationOutcome.issue.details.coding.code value.

[Example](Bundle-specialty-rx-query-response-error-1.html)

<br>