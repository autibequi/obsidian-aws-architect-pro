# Amazon Elastic Map Reduce #focus 
- Creates [[Hadoop Cluster]] (Big Data)
- Cluster made of 100s of [[AWS EC2#Instances]]
- Supports
	- Apache Spark
	- HBase
	- Presto
	- Flink
- All the provisioning as configuration of EC2 made by AWS
- Auto Scaling with [[CloudWatch]]
- Cases
	- Data Processing
	- Machine Learning
	- Web indexing
	- Big Data

## Integrations
![[Pasted image 20220417162919.png]]
- Launche in a VCP
- single AZ 
- HDFS - Temporary
- [[AWS S3]] - Persistent
	- via EMRFS #focus 

## Node Types & Purchasing
- Master node
	- Manage the cluster
	- coordinate
	- manage health
- Code Node
	- Run tasks
	- store data
- Task Node (optional)
	- Just run tasks 

- Purchasing Options
	- [[AWS EC2### EC2 Instances Launch Types

- Instance Configuration
	- Uniform Instance Groups
		- Single ___ for each node 
			- Instance Type
			- purchase option
		- Has Auto Scaling 
	- Instance Fleet
		- Select Target Capacity
		- mix 
			- instance types
			- purchase option
		- No Auto Scaling 