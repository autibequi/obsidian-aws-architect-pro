# AWS Config
- Helps auditing and recording compliance of AWS resources
- Records configurations and change over time
- Does not prevent actions from happening (no deny)
- You can receive alerts (SNS notification) for any changes
- per-region service
- Can be aggregated across regions and accounts

## Resource #focus
![[Pasted image 20220414173916.png]]

## AWS Config Rules
- Over 75 AWS managed config rules
- Can make custom config (using AWS Lambda)
- Rules can be evaluated/trigged
	- For each config change
	- and/or at regular time intervals
	- can trigger cloudwatch events if the rule is non-compliant (an chain with a lambda)
- Rules can have auto remediations
	- Define the remediation through [[SSM Automations]]
	