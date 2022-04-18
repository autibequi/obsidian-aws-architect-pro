# CloudWatch Logs
- get data to cloudwatch logs
	- SDk
	- CloudWatch Logs Agent
	- CloudWatch Logs Unified Agent
	- [[Elastic Beanstalk]]
	- [[AWS Lambda]]
	- [[AWS VPC#Flow Logs]]
	- [[AWS API Gateway]]
	- [[AWS CloudTrail]]
	- [[AWS Route 53]]

- Concepts
	- Log Groups
		- arbitrary name
		- usaully representing an application
	- Log Streams
		- Instance within an application 
		- log files
		- containers
	- Can define log expiration policies
		- never expire
		- expire 30 days
	- Optional KMS encryption
	- Can send data to other destionations
		- [[AWS S3]]
		- [[AWS Kinesis Stream]]
		- 

Data Export
- S3 bucket must be encrypted AWS-256 (SSE-S3) not KMS
- Can take 12h to teh data be avaiable to export
- api cal is `CreateExportTask`
- For real-time use log subscription instead

## Log Subscription
- ![[Pasted image 20220417223334.png]]

## CloudWatch Logs Agend & Unified Agent
- For virtual servers (EC2 Instances, on premise server)
- CloudWatch Log Agend
	- old version
	- can only send to [[CloudWatch Logs]]
- CloudWatch Unified Agent
	- Collect additional system-level metrics
		- ram
		- process
		- etc
	- can also send logs to [[CloudWatch Logs]]
	- centralized config using [[AWS SSM Parameter Store]]
- Batch Send (for both) #focus 
	- batch_count 
		- numero of log events sents (default 10.000, 1min)
	- batch_duration
		- duration of batching  for log events (default and min 5000ms)
	- batch_size
		- max size of log event in a batch (default & max is 1 MB)
		- 
- **Both agents cant send to Kinesis**
- **TO send data to kinesis you must use the kinesis agent instead**
- 