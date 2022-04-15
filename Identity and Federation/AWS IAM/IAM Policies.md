## IAM Policies
* Policies
	* AWS Managed
	* Customer Managed
	* Inline Policies
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