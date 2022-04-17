# AWS Aurora
- Engines
	- PostgreSQL
	- mySQL
- Storage
	- Automatically grows
		- up to 128 TB
	- 6 copies of data
		- Over 3 AZ
		- 4/6 for write
		- 3/6 for reads
	- Multi AZ
- Self-Healing 
- Automatically Fail Over of master
	- under 30 seconds
- Read-Replicas
	- up to 15 + master
	- single endpoint to read them all
- Cross-Region Replication
	- Entire DB is copied 
- load/off load directly to S3
- Backup
	- Same as RDS

## AWS Aurora Serverless
- Automatic
	- Scaling
	- Instantiation
- Good for workloads that are
	- infrequent
	- intermitent 
	- unpredicable
- No need for capacity planning
- Pay per second

## Global Aurora
- Aurora Cross Region Read Replica
	- [[Disaster Recovery]]
	- Simple to setup
- Aurora Global Database
	- 1 primary region (read/write)
	- up to 5 read-only regions
	- replication lag under 1 second
	- up to 16 read replicas per region
	- less latency
	- can promote region to master
		- [[Disaster Recovery#RTO]] under 1 minute

## Aurora Multi Master
- If you need imediate failover for Write
- Every node does r/w

## Aurora Endpoints
- Endpoint = Host Address + Port
- Cluster Endpoint
	- Writer Endpoint 
	- Primary DB Instance
	- Used for all writes
- Reader Endpoint
	- Provides load-balancing for read replicas only
	- Used only for Reads/queries
- Custom Endpoint #focus 
	- Used when to connect to a subset of the DB Instances
- Instance Endpoint
	- used to connect to a specific instance

![[Pasted image 20220416171840.png]]


## Aurora Logs
- Monitor the following log files:
	- Error Logs
	- Slow Query Logs
	- General Logs
	- Audit Logs
- They can be downloaded or published to [[CloudWatch Logs]]
- 