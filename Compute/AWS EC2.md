# EC2 - Elastic Cloud Computing
```toc
```

## Instances Types
| Letter          | Application           | Use Case          |
| --------------- | --------------------- | ----------------- |
| R               | App needs lots of RAM | in-memory caches  |
| C               | Need god CPU          | Compute Databases |
| M               | Balanced (medium)     | general / webapps |
| G               | Needs a GPU           | Machine Learning  |
| T2/T3           | Burstable Instances   |                   |
| T2/T3 Unlimited | Unlimited Bursts      |                   |
## Placement Group
- Controls where the EC2 Instance (virtual machine) will be placed in the datacenter
### Group Strategies
- You can move an instances in or out a group
	- First you stop
	- Use CLI to modify-instance-placement
	- Start the instance again

#### Cluster
- Instances deployed in a low latency group in a single AZ
- low latency 
- 10Gbps Bandwiths between instances
	- To use 100% of the bandwith select instances that have [[Enhanced Networking]]
- Cons
	- If Rack Fails, all instances fail at the same time

![[Pasted image 20220414184547.png]]

#### Spread
- Spread instances across underlying hardware
- Not the same Rack
- Max of 7 instances per group
- Critical applications

![[Pasted image 20220414184604.png]]

#### Partitions
- Spread accross many partitions
- Each partitions is a different set of racks
- Withing same AZ
- Scales up to 100 Instances per Group

![[Pasted image 20220414184615.png]]

## EC2 Instances Launch Types
### On-Demand 
* Short workload
* Predictable Pricing
* Reliable
### Spot Instances
* Short Workloads
* for cheap
* can lose instances
* not reliable
### Reserved  Instances
- Minimium 1 year
* Reserve Instances:
	* Long Workloads
* Convertible Reserved
	* long workload
	* flexibles instancees (convertabled)
* Dedicated Instances
	* No other customer will share your hardware
* Dedicated Host
	* Book and entire physical server
	* Control instance placement
	* **Host Affinity** #focus 
		* When affinity is set to host and the instance is not associated with a specific Dedicated Host, the next time the instance is launched, it is automatically associated with the host on which it lands. If the instance is restarted or rebooted, this relationship persists.

## EC2 Included Metrics
- CPU
	- Utilization
	- Credit
	- Balance
- Network
	- In
	- out
- Status Check
	- Instance Status - Check EC2 VM
	- System Status - Checks Hardware
- Disk - Instance Store
	- Read ops/bytes
	- Write ops/bytes
- RAM IS NOT INCLUDED

## EC2 Intance Recovery
- Status Check if Fail in 
	- Instance Level
	- Hardware Level
- Launch CloudWatch Alarm => Recovery instance
- All lost but recovery
	- Same Private, public IP
	- Elastic IP
	- Metadata
	- Placement Group