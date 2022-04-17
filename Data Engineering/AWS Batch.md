# AWS Batch
- Run batch jobs as Docker images
- Two options
	- Run on [[AWS Fargate]]
	- Dyamically instance provisioning ([[AWS EC2#Spot Instances]]) in [[AWS VPC]]
- Serveless
- pay per underlying resources used
	- fargate
	- ec2
- Schedule Jobs using [[CloudWatch Events]] or [[Amazon Event Bridge]]
- Orchestrate using [[AWS Step Function]]

## [[AWS Batch]] vs [[AWS Lambda]]
- Lambda
	- Time limit
	- Limited Runtimes
		- built in runtimes
		- docker images made for lambda
	- Limited temporary disk space
	- serverless
- Batch
	- no time limit
	- any runtime (just have to be a docker image)
	- rely on [[AWS EBS]] and [[AWS EBS & Instance Store]]
	- rely on EC2
		- can be managed by AWS
		- [[AWS Fargate]]

## Compute Environments
- Managed Compute Environment
	- [[AWS Batch]] manage the
		- capacity
		- instance types
			- set max min vCPU
		- can chose
			- on demand instances
			- spot instances
				- can set maximum price for spot instances
	- Launch within you VPC
		- Make sure to have access to [[AWS Elastic Container Service]] if inside a private subnet
			- use a NAT gateway / instance
			- [[VPC Endpoint Gateway]] for ECS
- Unmanaged Computer Environment
	- You control management
		- instances
		- provisioning
		- scaling 

## Multi Node Mode #focus 
- Large scale
- Good for [[High Peformance Computing]]
- Leverage multiple  EC2/ECS instances same time
- Good for tighly coupled workloads
- Represents a single job
- specify how many nodesf or the job
- 1main node manage the other child nodes
- Dont work with spot instances 
- works better if [[AWS EC2#Cluster]] placement group
	- because of [[Enhanced Networking]]
	- 