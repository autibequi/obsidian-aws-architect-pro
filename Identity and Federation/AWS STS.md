# STS
## Using STS to Assume a Role
* Define a [[IAM Role]]
* Define which principals can access this [[IAM Role]] 
* Use AWS STS to retrieve credentials for this role (AssumeRole API)
* Temp Credentials valid between 15min to 12 hours
* Reveko Active Session with: [[AWSRevokeOlderSessions]]
* When assuming role you lose your original permissions
* Benefits
	* Explicity grant your users permission to assume the role
	* You can add [[MFA protection]]
	* Least Privilege
	* Auditing using [[AWS CloudTrail]]

## Cross Account Access with STS
![[Pasted image 20220413152423.png]]

### Providing Access to AWS Account Owned Third Parties
* Zone of trust = account, org that you own
* Outised Zone of Trust= third parties
* Use [[IAM Access Analyzer]] to find out which resources are exposed
* For granting access to third party:
	* Third Party AWS Account ID
	* An External ID (secret between you and third party)
## The Confused Deputy #focus
![[ConfusedDeputy.png]]

* Use the external ID as a password to avoid attacks that hve the same ARN name

## STS Important APIs
* AssumeRole:
* AssumeRoleWIthSAML: for users logged in SAML
* ASsumeRoleWithWebIdentity: for users logged via oauth2 (AWS Recommends Cognito instead)
* GetSessionToken: for MFA from users
* GetFederationToken: get temporary creds for a federated user (usually a proxy app that will validate user and gen credentials from aws)