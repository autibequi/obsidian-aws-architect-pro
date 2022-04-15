# AWS Orgainzations
#identity_and_federation
- Root Organziation Unit (OU)
- Management Account
- Member Account
- OrganizationAccountAccessRole
	- Allow full admin permission to the Member Account
	- Use to perfrom admin tasks (create iam users etc)
	- Automatically Created When Member account is created via AWS Organization
	- Must be created manully if Account was already created and invited to AWS Org
- Features Modes
	- Consolidated Billing
		- Consolidated Billing - Single Payment
		- Princing benefit from agrgregated usage
	- All Feature
		- Includes consolidated Billing features
		- SCP
		- Invited accounts must approve enabling all features
		- Ability to apply an SCP to prevent member accounts from leaving the org
		- can't switch back to Consolidated Billing Features Only
- Reserved Instance
	- Will be valid accross all OU
	- The Payer Account (Management Account) of an Org can turn off this  Reserved Instance discoutn and saving plans discounts sharing for any account in that organization, including the payer account.

## Service Control Policies (SCP)
* Define allow list or blocklist IAM Actions
* Applied at OU or Account level
* Does not apply to the Management Account
* SCP is applied to all Users and Roles (including Root User)
* The SCP does not affect Service Linked Roles #focus 

## IAM Policy Evaluation Logic
![[Pasted image 20220414125940.png]]

## Restricting Tags with IAM Police
- Restrict a police bansed on conditions
- Condition is "has a tag" else not allowed
- Policy Conditions #focus 
	- ForAllValue
	- ForAnyValue

## Tag Policies
- Helps standardize tags across resources in an AWS Org
- You define tag keys and their allowed values
- Helps wiht AWS Cost allocation tag 
- Avoid any non compliant tagg
- Create report based on compliance

## AI Service Opt-Out Policies
- SOme services collect data to AI/ML to improve services
	- Lex
	- Comprehen
	- Polly
- You cant opt-out

## Backup Policies #focus 
## AWS Resource Access Manager (RAM)
* Share AWS Resources with other AWS Accounts ou AWS Orgs
* Avoid duplication
	* VPC Subnet
		* Must be from the same AWS Org
		* Cannot share security groups and default vpc
		* Can only manage own resources
		* Cannot view modify delete resource of other participants
	* Transit Gateway
	* Route 53
	* License Manager Configurations 
	* Aurora DB
	* ACM Private Certioficate
	* CodeBuild Project
	* EC2
	* AWS Glue
	* AWS Network Firewall Policies
* etc etc etc
### VPC Example
![[Pasted image 20220414135316.png]]

