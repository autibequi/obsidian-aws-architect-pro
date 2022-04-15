# API Gateway
- Helps expose
	- Lambdas
	- HTTP
	- AWS Services as an API
- API Versioning
- Authorization
- Traffic Management
	- API Keys
	- throttles
- Huge Scale
- #Serverless
- Req/Resp Transformation
- OpenAPI spec
- CORS
- **Limits to know**
	- 29 seconds timeout
	- 10 MB Max Payload Size

## Deployment Stages
- API changes are deployed to "Stages"
- Use the namingyou like for stages
- Stages cna be rolled back

## Integrations
- HTTP
	- Expose HTTP endpoints in the backend
	- Example
		- Internal HTTP API on premise
		- [[Application Load Balancer]]
	- Why?
		- Add 
			- rate limiting
			- caching
			- user authentication
			- API Keys
			- etc
- Lambda Function
	- Invoke Lambda function
	- Easy way to expose REST API backed by AWS Lambda
- AWS Service
	- Expose any AWS API through the API Gateway
	- Example
		- start an AWS Step Function workflow
		- post a message to SQS
	- Why?
		- Add Authentication
		- Deploy publicly
		- Rate Control

## Endpoint Types
- Edge-Optmized
	- Default
	- For global clients
	- Request are routed through the CloudFront Edge Location (improves latency)
	- The API Gateway still lives in only one region
- Regional
	- For clients within the same region
	- Could manully combine with CloudFront
		- More control over the caching strategies and distribution
- Private
	- Deploy only inside a VPC
	- Use a [[Resource Based Policies]] to define access

## Errors
- 4XX - Client Errors
	- 400 - Bad Request
	- 403 - Access Denied, WAF Filtered
	- 429 - Quota exceeded, Throttle
- 5XX - Server Errors
	- 502 - Bad Gateway Exception
		- Usually incompatible output returned from lambda proxy
		- occasionally for out of order invocations due to heavy loads #focus 
	- 503 - Service Unavailable Exception
	- 504 - Integration Failure
		- Endpoint Request Timed-out Exception
		- API Gatway requests time ou after 29 seconds maximum 

## Security
- Load SSL certificates
- Use Route53 to define CNAME
- [[Resource Based Policies]]
	- ~S3 Bucket Policy
	- Users fromA WS account
	- IP or CIDR block
	- VPC
	- VPC Endpoints
- IAM Execution Roles for API Gateway at API level
	- To invoke 
		- a Lambda function
		- an AWS Service
- [[Cross-Origin resource sharing]]

## Authentication
- IAM Based Access
	- Good for providing acces within you own infra
	- Pass IAM credentials in headers through Sig V4 #focus 
- Lambda Authorizer (formerly Custom Authorizer)
	- Use Lambda to verify acustom OAuth/SAML/third party authentication
- Cognito user Pools
	- Client authenticates with Cognito
	- Client passes the token to API Gateway
	- API know how to validate the token out of the box

## Logging, Monitoirng, Tracing
- [[CloudWatch Logs]] 
	- Enable log at stage level
	- Can log full req/res data
	- Can send API Gateway Access Logs
	- Can send logs directly into  [[Kinesis]] Data Firehose (alternative to CW Logs)
- [[CloudWatch Metrics]]
	- Metrics are by stage
	- Possibility to enable detailed metrics
- [[X-Ray]]
	- Enable tracing to get extra info

## Usage Plans & API Keys
- If you want to make an API Avaiable as an offering (money) to customers
- **Usage Plan**:
	- Who can access one or more API stage or methods
	- how much and how fast can access them
	- use **API keys** to identify clients and meter access
	- configure throttlinglimits and quota limits

## WebSocket API
- Two-way interactive communication between client and server
- Server can push information to the client
- Enables stateful application use case
- Useful for **real-time applications**
	- collaboration plataform
	- multiplayer games
	- financial trading
- Works with AWS Services 
	- Lambda
	- DynamoDB
	- HTTP Endpoints

![[Pasted image 20220415134915.png]]

![[Pasted image 20220415135044.png]]