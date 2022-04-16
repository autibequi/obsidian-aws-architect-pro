# S3 Security
```toc
```
## S3 Encryption for Objects #focus
- SSE-S3
	- Encrypts S3 objects using keys managed by AWS
- SSE-KMS
	- Encrypts using keys provided by KMS
- SSE-C
	- When you want to maange your own encryption key
- Client Side Encryption
	- You encrypt in client
- Glaciers
	- All that is AWS256 encrypted key under AWS Control
## Encryption in transit (SSL)
- AWS S3 exposes
	- HTTP (no encrypted)
	- HTTPS (encrypted in flight)
		- Mandatory for SSE-C

## Event in S3 Buckets
- S3 Access Logs
	- all requests that are made to the bucket
	- might take hours to deliver
	- might be incomplete (best effort)
- S3 Event Notification
	- events like CRUD 
	- destination
		- SNS
		- SQS
		- Lambda
	- Delivered in seconds
		- If versioning enabled: a event is sent for each file same name
		- if disabled: you may receive only one notification for two files saved with the same name (and folder)
	- Trust Advisor
		- Check bucket permission to access it
	- CloudWatch events
		- Need to enable cloudtrail object levl logging on s3 first
		- target:
			- lambda 
			- sqs
			- sns
			- etc

## Security
- User based
	- IAM Policies
- Resource Based
	- Bucket Policies - allow crossaccountr
	- Object Access Control List - Finer grain
	- Bucket Access Control List - less common

## S3 Bucket Policies
- Use S3 buckets for
	- grant public access
	- force objects to be encrpted
	- grant access to another accound
- Optional Condition on:
	- public IP or Elastic IP (NOT PRIVATE IP)
	- source VPC or Source VPC endpoint
	- [[AWS CloudFront]] Origin Idenity
	- MFA

## S3 Pre-signed URL
- Can generate presigned URL using SDK or CLI
	- for download
	- for upload
- valid for 3600seconds default
	- can change it on creation
- Users given the URL inherit the permissions of the user generated the GET / PUT

## S3 Object Lock & Glacier Vault Lock
 - S3 Object Lock
	 - Adopt a WORM (write once read many) model
	 - Block an objet version deletion for a specified amount of time
- Glacier Vault Lock
	- Adopt a WORM model
	- Loick the poilicy for future edits (can no longer be changed)
	- Helpful for compliance and data retention