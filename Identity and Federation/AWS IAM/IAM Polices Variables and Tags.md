## IAM Polices Variables and Tags
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