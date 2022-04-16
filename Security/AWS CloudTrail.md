# AWS CloudTrail
- Provide governance, compliance and audit
- Enable by Default
- Stored for 90 days
	- To keep more than that migrate them to s3
	- analyze s3 via athena
- Get a history of events /apicalls made within AWS Account
	- Console
	- SDK
	- CLI
	- AWS Services
- Can save CloudTrails to
	- S3
	- CloudWatch Logs
- Can apply to
	* all REgion (default)
	- Single Region 
* Events
	* Management Event
		* Operation that performed to resources
		* Enabled by Default
		* Can be
			* Write
			* Read
	* Data Event
		* Disable by default (because of hi volumes)
		* Example:
			* S3 getObject, DeleteObject, PutObject
			* aws lambda function execution
		* Can be
			* Read
			* write
	* CloudTrail Insight Trails

## CloudTrail Insight
- Helps detect unusual activity
	- Innacurate resource provisioning
	- hitting servcie limits
	- burst of aws iam action
	- gaps in periodic maintenance activity
- Analyz Normal Management events to create baseline
- Continuously analyze write events to detect unusual patterns
- Anomlies appears on 
	- cloudtrail console
	- s3
	- eventbridge

## Organizational Trail
An account dedicated to receive all CloudTrail form other accounts from an AWS Org

## React to CloudTrail Events
- CloudWatch Event
	- Faster More Reactive
	- can be trigger for any api call in cloudtrail
- CloudTrail Delivery in CloudWatch Logs
	- Events are streamed
	- can perform a metric filter to anlyze occurrences and detect anomalies
- Delivery to S3
	- Events are deliverd every 5min
	- For analyzing logs, long term storage
- 