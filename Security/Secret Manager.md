# AWS Secret Manager
- Meant to store password api key etc
- Can force rotation
	- Atomate generation of secrets
	- natively supports
		- Amazon RDS
		- Redshift
		- DocumentDB
		- Lambda
		- etc
	- Controll acesst o ecret using resource based policy
	- Integration with other AWS servcies
		- CloudFormation
		- CodeBuild
		- ECS
		- EMR
		- Fargate
		- EKS,
		- Parameter Store

[[SSM Parameter Store]] vs[[Secret Manager]]

* Secret Manager 
	* More expensive
	* Automatic rotation (via provided lambda)
		* RDS
		* Redshift 
		* documentdb
	* KMS encryption is mandatory
	* Can integrae with CloudFormation
* Parameters Store
	* Cheaper
	* Simple API
	* No Secret Rotation
	* KMS optional
	* can pll a secret manager using a parametr store #focus 
* 