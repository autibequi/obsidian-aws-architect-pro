# AWS Lambda
## Main Integrations
- [[API Gateway]]
- [[Kinesis]]
- [[DynamoDB]]
- [[S3]]
- [[IoT]]
- [[CloudWatch Events]] 
- [[CloudWatch Logs]]
- [[SNS]]
- [[Cognito]]
- [[SQS]]

## Runtimes
- Node
- Python
- C#
- Golang
- C#
- Ruby
- Custom Runtime API
	- Rust
- Lambda Container Image #focus 
	- Te container image must implement tha Lambda Runtime API

## Limits
- RAM - 128 to 10,240MB
- CPU
	- linked to CPU
		- 2 vCPU are alocated at 1,769 MB
		- 6 vCPU are alocated at 10,240 MB
- Timeout - up to 15min
- /tmp Storage - 512MB
- Deployment Package
	- 50MB zipped
	- 250MB unzipped
	- Including Layers
- Concurent Executions - 1000 (soft)
- Container Image Size - 10GB
- Invocation Payload (req/response)
	- 6MB Sync
	- 256KB Async
- Invocation Payload

## Latencies Considerations
![[_imgs/Lambda_Latency.png]]

## Security
- [[IAM Role]]s for Lambda
- [[Resource-based Policies]] for Lambda
	- Similar to [[S3 Security#S3 Bucket Policies]]
- VPC
	- Runs on a AWS Cloud VPC by default
	- Cant access any resource in another private VPC
	- Solution
		- Deploy Lambda inside a VPC
		- Blocks 
			- Internet access
			- Access to Public Services
				- DynamoDB
				- [[S3]] 
				- etc
		- Needs 
			- a [[NAT Gateway]] connected to a [[Internet Gateway]] to access the internet
			- or a [[VPC Endpoint Gateway]] to access AWS Public Services
- CloudWatch Logs works even without endpoint or NAT Gateway

## Logging, Monitoring & Tracing
- [[CloudWatch]]
	- Execution logs are stored in [[CloudWatch Logs]]
	- Metrics are displayed in [[CloudWatch Metrics]]
		- Successful invocation
		- error rates
		- latency
		- timeout etc
	- Makes sure Lambda Role have permission to write to CloudWatch Logs
- [[X-Ray]]
	- Possible to trace Lambda with X-Ray
	- Enable 
		- in Lambda Configuration (Managed)
		- Use SDK in Code

## Synchronous Invocations
- Via
	- CLI
	- SDK
	- [[API Gateway]]
- Results are returned right away
- Error handling must happen cient side
	- retries
	- [[exponential backoff]]
	- etc

## Asynchronous Invocation
- Via
	- [[S3]]
	- [[SNS]]
	- [[CloudWatch Events]]
- Lambda auto retries 3 times
	- Make sure the processing is [[idempotent]] in this case
- Can define queues for failed processing
	- [[Dead Letter Queues]]
	- SNS 
	- SQS

## Event Source Mapping
- Source
	- [[Kinesis]] Data Streams
	- [[SQS]]
	- [[SQS FIFO]]
	- [[DynamoDB]] Streams
	- [[Amazon MQ]]
	- [[Apache Kafka]]
- All records repect ordering 
	- Except [[SQS]] Standart
- If your function returns an error the entire batch is reprocessed until success
	- [[Kinesis]],[[DynamoDB]] Stream: stop shard processing

## Destination #focus 
* Nov 2019 - Can configure to send result to a destination
* Async Invocations
	* https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html
	* Define destination for
		* success event
		* failed event
	* Destinations 
		* SQS
		* SNS
		* Lambda
		* [[Amazon Event Bridge]]
* ==AWS recomends you to use destination instead of [[Dead Letter Queues]]. Both can be used at the same time==
* Event Source Mapping
	* https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html
	* Only for discardedevent batches
	* Destinations
		* [[SQS]]
		* [[SNS]]

## Lambda Version
- Always work on the `$LASTEST` version
- Publishing a lambda creates a new version
- Versions are immutable
- Version have increasing number
- Versions get their own [[ARN]]
- Version = Code + Configuration + EnvVar

## Lambda Alias
- Pointers to lambda functions
- Alias are mutable

## Lambda Alias with [[API Gateway]]
![[Captura de Tela 2022-04-14 às 22.41.57.png]]

## Lambda & [[CodeDeploy]]
- CodeDeploy can help you automate traffic shift for lambda aliases
- Feature is integrated withing the [[SAM Framework]]
- Traffic Shift Modes
	- `Linear`: grow traffic every N minutes until 100%
		- Linear10PercentEvery3Minutes
		- Linear10PercentEvery10Minutes
	- `Canary`: try X percent then 100%
		- Canary10Percent5Minutes
	- `AllAtOnce`
	- You can create Pre & Post Traffic hooks to check health of the Lambda