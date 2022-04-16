# AWS EFS - Elastic File System
- Managed Network File System
- Can be mounted on many EC2 Instances
- Works in multi-az and on-premise (DX & VPN) #doubt
- Highly availabel
- scalable
- expenseive (3x gp2)
- pay per gb
- Use cases
	- Content management
	- web serving
	- data sharing
	- wordpress
- Compatbile with linuy bases AMI (**NOT WINDOWS**) 
- POSIX-compliant
- Use NFSv4.1 protocol
- Use security groups top control access
- Can only attach to one VPC
- Create one ENI (mount target) per AZ
- POSIX file system (LINUX) that has a standart file API
- File system scales automatically
- Pay-per-use
- No capacity planning 

## Performance Classes
- EFS Scale
	- 1000s of concurrent NFS client
	- 10GB+/s throughput
	- Grow to Pentabyte-scale network file system (automatically)
- Performance Mode (Set at EFS creation time)
	- General purpose (default)
		- latency-sensitive 
		- Cases
			- webserver
			- cms
			- etc
	- MAX I/O
		- Higher Latency
		- Throughput 
		- Highly parallell
		- Cases
			- Big Data
			- Media Processing
- Throughput mode
	- Bursting
		- 1TB gives 50MiB/s + burst of up to 100MiB/s
	- Provisioned
		- Set your throughput regardless of storage size

## Storage Classes
- Storage Tiers
	- Standart
		- For frequently access files
	- Infrequent Access (EFS-IA)
		- cost to retrieve files
		- lower price to store
		- Enable it with a Lifecycle Policy
- Availability and Durability
	- Regional
		- Multi-AZ
		- Great for Prod
	- One Zone
		- One AZ
		- Great for Dev/backup
		- enabled by default
		- compatible with Infrequent Access (EFS One Zone IA)

## Access Points
- Easly manage application access to NFS env
- Enforce POSIX user and group to use when accessing the FS
- Restrict access to a directory within the FS and opitonally specif a different root directory
- Can restrict access from NFS clietn using IAM Policies

## File System Policies
- [[Resource Based Policies]] to control access to EFS File Systems
- Full access to all clients by default