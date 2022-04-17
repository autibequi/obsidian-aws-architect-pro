# AWS Step Functions
- Serverless
- Visual Workflow
- For Lambda Archestration
- JSON
- Features
	- sequence
	- parallel
	- condition
	- timeout
	- error handling
	- etc
- Maximum time execution: 1year
- Possibility
	- Human approval feature
- Chaining Lambdas adds latency to the process

## Integrations
- Optimized Integrations
	- Can Invoke [[AWS Lambda]]
	- Run [[AWS Batch]]
	- Run [[AWS Elastic Container Service#Task Definitions]]
		- and wait to complete 
	- Insert iten to [[AWS DynamoDB]]
	- Launch
		- EMR
		- [[AWS Glue]]
		- [[AWS SageMaker]]
		- Another Step Function Flow
- SDK integration
	- anything you want 

## Triggers
- Management Console
- SDK
- CLI
- [[AWS Lambda]]
- [[AWS API Gateway]]
- [[Amazon Event Bridge]]
- [[CodePipeline]]
- [[AWS Step Function]]

## Tasks
- Lambda Tasks
- Activity Tasks
	- HTTP
	- EC2 Instances
	- Mobile Devices
	- On Premice Data Center
	- They poll the Step Function Service
- Service Tasks
	- Connect to AWS Services
	- Lambda
	- ECS Tasks
	- [[AWS Fargate]]
	- DynamoDB
	- BatchJob
	- SNS Topic
	- SQS Queue
- Wait tasks
	- Wait for a duration of time
- No integration with **AWS Mechanical Turk**
- 