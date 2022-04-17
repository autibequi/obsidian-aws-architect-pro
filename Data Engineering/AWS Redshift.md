# AWS Redshift
- Based on PostgreSQL
- Not used to [[OLTP]]
- It's [[OLAP]] - 
	- Online Analytic Processing
	- Analytics and Data Warehousing
- 10x better than other datawarehouses
- Scales to PBs of Data
- Colunar Storage of Data (instead of Row)
- MPP - Massive Parallel Query Execution
- Pay as you go
	- based on instances provisioned
- SQL Interface
- BI tools Integration
	- [[AWS QuickSight]]
	- Tableau #doubt 
- Data is loaded
	- [[AWS S3]]
	- [[AWS Kinesis Firehose]]
	- [[AWS DynamoDB]]
	- [[AWS DMS]]
- 100+ nodes
- up to 16TB per node
- **Not Multi-AZ**
- Types of node
	- Leader Node
		- query planning
		- result aggregation
	- Compute Node
		- performe queries
		- return data to the leader
- Backup & Restore
- [[AWS VPC]]
- [[IAM Policies]]
- [[AWS KMS]]
- Monitoring
- Redshift Enhanced VPC Routing
	- COPY / LOAD goes through VPC
		- Faster
		- less cost 
- Is provisioned
	- SO its worth it if you have a sustained usage
		- otherwise use [[AWS Athena]] is is sporadic use

## Snapshots & [[Disaster Recovery]]
- snapshots
	- point in time backup of a cluster
	- stored on [[AWS S3]]
	- are incremental
	- can restore snapshot to a new cluster 
	- types
		- automated
			- every 8hour
			- every 5GB
			- on a schedule
			- must set retention limit (ex 30days)
		- Manual
			- retained until deleted
	- Can be configured to be copied to another region
		- useful for [[Disaster Recovery]]

## Redshift Spectrum
- Query data from [[AWS S3]] without loading it
- Must already have a Redshift Cluster
![[Pasted image 20220417171009.png]]

## Redshift Workload Management (WLM)
- Allow priorityze queries
- prevest fast running queries to be stuck behing long-running queries
- Define multiple query queues
- Route Query to correct queue
- Types
	- Automatically WLM
	- Manual WLM

## Redshift Concurrency Scaling
- consistent fast performance
- virtually unlimited clients
- automatically add adicionar cluster capacity
	- Concurrency-Scaling Cluster
- Ability to decide which cluster will goes to Concurrency-scaling cluster using WLM