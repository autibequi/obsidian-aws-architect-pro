# Elastic Container Service
- Microservices
	- Run multiple docker containers same machine
	- Easy service discovery feature #focus 
	- Direct integration with [[Application Load Balancer]] and [[Network Load Balancer]]
- Batch Processing / Scheduled Tasks
	- Schedule ECS tasks to run on 
		- [[On-demand]]
		- reserved
		- [[Auto Scaling#EC2 Spot Instances|Spot Instances]]
- Migrate Applications to the Cloud
	- Dockerize legacy apps running on premise

## Concepts
### ECS Cluster
- Logical Grouping of EC2 Instances
### ECS Service
- Defines how many tasks should run an how they should be run
### Task Definitions
- metadata in JSON form
- tells ECS how to run a docker container
	- imagine name
	- cpu
	- ram
	- etc
- ECS Tasks
	- Instance of a task definition
	- a running docker container
- ECS IAM Role
	- EC2 Instance Profile
		- Used by the EC2 Instances to make API calls
	- ECS Task IAM Role
		- Allow each task to have specific role

![[Pasted image 20220414212416.png]]

## Dynamic Port Mapping
- Allows you to run multiples instances of the same app in thesame EC2 instance
- ALB will find hte right port on your EC2 Instances
- USe Cases
	- Increased resiliency even if running on one ec2 instance
	- Maximize utilization of CPU/Cores
	- Ability to perform rolling upgrades without impacting app uptime

## Security & Network
- You can inject secrets and configuration as envvar into running docker containers
	- Integration with [[SSM Parameter Store]]
- ECS Tasks Networking 
	- `none`
		- no network connectivity
		- no port mapping
	- `bridge`
		- uses docker's virtual container-based network
	- `host`
		- bypass docker's network
		- uses the underlying host network interface
	- `awsvpc`
		- every task launched on the instance gets its own ENI and private IP
		- simplified networking
		- enhanced security
		- security groups
		- mopnitoring
		- vpc flow logs
		- Default mode for Fargat tasks

## Service Auto Scaling #focus 
- Automatically scale the desired number of tasks
- ECS leverage [[Auto Scaling]]
- CPU and ARM is tracked in [[CloudWatch]]
- Scalings:
	- `Target Tracking`
	- `Step Scaling`
	- `Schedule Scaling`
- ECS Service Auto Scaling (tasks level)  != EC2 Auto Scaling (Instance Level)
- Fargate doesnt need to care about it (serverless)

## [[Auto Scaling#EC2 Spot Instances|Spot Instances]]
- ECS Classic (ec2 launch type)
	- Managed by an ASG
	- Instance may go into [[draining mode]] to remove running tasks
	- Good for cost saving
	- Will impact reliability
- [[Fargate]]
	- Specify minimm of tasks for on-demand baseline workload
	- Add tasks running on FARGATE_SPOT for cost-saving 
	- Regardless of on-demand or spot, fargate scales well based on load