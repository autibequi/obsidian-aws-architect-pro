# Identity Federation in AWS
#identity_and_federation
- Give users outside AWS permision to acess resources
- Don't need to manage IAM Users
- Can use another identity system 
	- SAML 2.0
	- Custom Identity Broker
	- Web Identity Federation 
	- SSO

![[Pasted image 20220414111128.png]]
## SAML 2.0 Federation
* Security Assertion Markup Language 2.0
* Open Standart
	* Support Integration with MS Active Directory Federation Services (ADFS)
	* or any SAML 2.0 compatible idPs
* Access to AWS Console, AWS CLI, AWS API using temporary credentials
	* No need to create IAM User for each employee
	* Need to setup a trust between IAM and SAML 2.0
* Under the hood
	* Uses STS API AssumeRoleWithSAML
* SAML 2.0 is the old way
* Amazon SSO Federation is the new managed and simpler way
### SAML 2.0
![[Pasted image 20220414111818.png]]

![[Pasted image 20220414111836.png]]

![[Pasted image 20220414111846.png]]

### Custom Identity Broker Applicaton
![[Pasted image 20220414111937.png]]
### Web Identity Federation - No Cognito
![[Pasted image 20220414112021.png]]
### Web Idenity Federation - With Cognito
![[Pasted image 20220414112044.png]]

## IAM Policy
* After authenticated with Federation you can idenitify users via IAM Policy Variables
* ${www.amazon.com:user_id}
* ${graph.facebook.com:id}
* ${account.google.com:sub}
* ${cognito-idenitity.amazonaws.com:sub}