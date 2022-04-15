# IAM
#identity_and_federation
* Users: long term credentials
* Groups: contain User
* [[IAM Role]]: short-term credentials, uses STS
	* EC2 Instance Role
		* One Role Per Instance
	* Service Roles
		* API Gateway
		* Code Deploy
	* Cross Account Role
* Policies
	* AWS Managed
	* Customer Managed
	* Inline Policies
* [[Resource Based Policies]]
	* S3 bucket
	* SQS queue

## IAM Policies
* JSON doc
	* Effect
	* Action
	* Resource
	* Conditions
	* Policy Variables
* Explicit DENY precendece over ALLOW
* Best Pratice
	* Use least privilege for maximum security
		* Access Advisor: See permissions granted and when last accessed
		* Access Analyzer: Analyze Resource that are shared with external entity
* Police Conditions
	* String
	* Numeric
	* Date
	* Boolean
	* (not) IpAddress
	* ArnEquals
	* ArnLike
	* Null
## IAM Police Variables and Tags
* ${aws:username}
* AWS Specific
	* aws:CurrentTime
	* aws:TokenIssueTime
	* ...
* Service Specific
	* s3:prefix
	* s3:max-keys
	* s3:x-amz-acl
* Tag Based
	* iam:ResourceTag/key-name
	* aws:PrincipalTag/key-name
## IAM Role vs [[Resource Base Policies]]
![[Pasted image 20220413143931.png]]

* When assuming a role you lost all yours account original permissions
## IAM Permission Boundaries
* Define the maximum permission an IAM entity can get
![[PermissionBoundaries.png]]
