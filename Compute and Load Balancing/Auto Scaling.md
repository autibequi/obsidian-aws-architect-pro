# Auto Scaling 
## Auto Scaling Groups
### Dynamic Scaling Policies
* Target Tracking Scaling
	* Most simple and easy to set-up
	* Example:
		* I want the average ASG CPU to stay arround 40%
	* Simple / Step Scaling
		* When CloudWatch alarm is trigged (CPU > 70%)
			* Then add 3 units
		* When CPU < 30%
			* Remove 1 unit
	* Schedule Actions
		* Anticipate a scaling based on known usage patterns
		* Example: 
			* increase the min capacity to 10 at 5pm on Fridays
* Predictive Scaling
	* Continuously forecast load and schedule ahead
* Good Metrics to scale on
	* CPUUtilization: Average CPU utilization across you instances
	* RequestCountPerTarget: make sure the number of request per EC2 is stable
	* Average Network In/Out
	* Any Custom CloudWatch Metric
* Good To Know
	* Spot Fleet Support
		* Mix on spot and on-demand instances
	* Lifecyle Hooks
		* Perform actions before an instance is in service ir before it is terminated
	* To upgrade an AMI
		* Muyst update the launch configuration / template
		* then 
			* terminate the old instances manually
			* or use EC2 Instance Refresh
* [[EC2 Instance Refresh]]
	* Goal
		* Update launch template
		* recreate all ec2 instances
	* Set minimum healthy percentage
	* specify warm-up time ( how long until instance is ready to use )

## Scaling Process
* Launch
	* Add a new EC2 instance
	* Increase the ASG capacity
* Terminate
	* Remove an EC2 Instance
	* Decrease ASG capacity
* HealthCheck
	* EC2 Status Cehck
	* ELB Health Check (HTTP)
* ReplaceUnhealthy
	* Teminate Unhealthy Instances and recreate them
* AZRebalance
* AlarmNotification
* ScheduleAction
* AddToLoadBlancer
* InstanceRefesh

All process can be suspended for debuging etc

## EC2 Spot Instances
- Up to 90% discount over on-demand
- Define `max spot price` and get instances while `current spot price < max`.
	- The hourly spot price varies 
	- if the current spot price > your price you can chose to `stop`or `terminate` your instance with a 2 minute grace period.
- Use for 
	- batch jobs
	- data abalysics
	- workloads that are resilient to failure
- Not great for
	- critical jobs
	- databases

## EC2 Spot Fleets #focus 
- Collection of Spot instances 
	- Optionally on-demand too
- Set a maximum price
	- per spot instance
	- for all instances
- Can have a mix of instances types
- Supports
	- EC2 Standalone
	- Auto Scaling group (launch template)
	- ECS (underlying ASG)
	- AWS Batch (managed compute Env) #focus 
- Soft Limit
	- per spot fleet or ec2 fleet: 10.000
	- across all spot fleet and ec2 fleet in a region: 100.000
- Will try to meet the target with price constrains
	- define possible launch pools
	- Can hve multiple launch pools to be choosen by the fleet
	- spot fleet stop launching instances when reaching capacity or max cost
- Strategies to allocate spot instances
	- `LowestPrice`: 
		- Will launch from the pool with the lowest price
		- good for optimization and short workloads
	-`diversified`
		- distributed across all pools
		- good for availability and long workloads
	- `capacityOptimized`:
		- pool with the optimal capacity for the number of instances