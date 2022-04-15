# IAM
* Users: long term credentials
* Groups: contain User
* [[IAM Role]]: short-term credentials, uses STS
	* EC2 Instance Role
		* One Role Per Instance
	* Service Roles
		* API Gateway
		* Code Deploy
	* Cross Account Role

* When assuming a role you lost all yours account original permissions
