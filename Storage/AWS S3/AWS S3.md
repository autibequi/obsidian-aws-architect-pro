# AWS S3
- Object Storage
- Serverless
- Unlimited Storage
- Pay as You go
- Good to store static content
	- image
	- video
- Access objects by key
- no indexing facility
- Not a filesystem
- connot be mounted natively on EC2

## Anti Patterns
- Lots of small files
- POSIX file system (use [[AWS EFS]] instead)
- File Locks
- Seach features
- Queries 
- Rapidly changing Data
- Website with dynamic content

## S3 Storage Classes Comparsion
![[Pasted image 20220415200434.png]]

## Replication
- Cross Region Replication
- Same Region Replication
- Combine with Lifecycles Policies
- Cases
	- Reduce Latency
	- [[Disaster Recovery]]
	- Security
- S3 Bucket Versioning must be eneabled

## Event Notifications
- S3 CRUD
- Object name Filtering possible (\*.jpg)
- Case
	- Generate Thumbenails upload to S3
- Can create as manyu "S3 Event" as desired
- Typically deliver events inseconds but can sometimes take a minute or longer
- targets
	- [[AWS SQS]]
	- [[SNS]]
	- ...

### With Amazon EventBridge
- Send S3 events to [[Amazon Event Bridge]]
- Create complex rules there
- Advanced Filtering options with json rules
	- metadata
	- object size
	- name
	- etc
- Multiple Destinations
	- Step functions
	-  [[AWS Kinesis]] Streams
- EventBridge Capabilities
	- Archieve
	- Replay Event
	- Reliable Delivery

## Baseline Performance
- S3 automatically scales to high requests rates
- latency 100-200ms
- Can archieve at least XXX requests per second per prefix in a bucket
	- 3500 PUT/COPY/POST/DELETE
	- 5500 GET/HEAD 
- There is no limits ot the number of prefixes in a bucket
- Upload
	- Multi-Part Upload
		- Recomended for > 100MB
		- MUST USE for > 5GB
		- Can help parallelize uploads (higher speeds)
		- Remove Incomplete Parts
			- Use Lifecycle policy to abort and delete incomeplete multipart uploads after x days
	- S3 Transfer Acceleration
		- Upload Only
		- Increase Transfer Speed by transfer the file to an [[AWS CloudFront#Edge Locations]]
		- Can be combined with multi-part
- Download
	- S3 Byte-Range Fetches
		- Parallelize GETs b y requesting specific 
		- Better resilience in case of failure
		- Cases
			- Faster download
			- Download only part of a file

## S3 Select & Glacier Select
- Retrieve Less data usign SQL by performing server side filtering
- Can Filter by rows and Columns (Simple SQL Statement)
- Less Network transfer
- Less CPU client-side