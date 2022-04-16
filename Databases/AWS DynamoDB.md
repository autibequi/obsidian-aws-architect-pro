# AWS DynamoDB
```toc
```
- NoSQL
- Fully managed
- Massive Scale (1.000.000 rps)
- Similar to Apache Cassandra
	- Can migrate to DynamoDB
- No Disk space to provision
- max object 400KB
- Capacity
	- Provisioned
		- WCU
		- RCU
		- Auto Scaling
	- On Demand
- Supports CRUD
- Read: Eventually or Strong consistency
- Supports transactions across multiple tables 
- ACID Support 
- Backups Available
	- Point in time recovery
- Table classes
	- Standart
	- Infrequent Access (IA)

## Basics
- Made of Tables
- Each table has a primary key
	- Decided at creation time
- Can have infinite number of itens (rows)
- Each item has attributes 
	- can be added over time
	-  can be null
- Maximum item size 400KB
- Data types
	- Scalar types
		- String
		- NUmber
		- Binary
		- Boolean
		- Null
	- Documnet Types
		- List
		- Map
	- Set Types
		- String Set
		- Number Set
		- Binary Set

### Primary Keys
- Option 1 
	- Partition Key Only (HASH)
	- unique for each item
	- key must be "diverse" so the data is well distributed
		- example
			- User_Id for a users table
- Option 2
	- Partition Key + Sort Key
	- Combination of two is unique
	- Data is grouped by partition key
	- Sort key === Range Key

### Indexes
- Object = Primary Key + optional sort key + Attributes
- LSI - Local  Secondary Index
	- keep the same primary key
	- select an alternative sort key
	- Must be defined at creation time
- GSI - Global Secondary Index
	- Change the primary key and optional sort key
	- Can be defined after the table is created
- You can only query by
	- PK + Sort Key on main table
	- Indexes (different than RDS)

### Important Features
- TTL
- DynamoDB Stream
	- react to changes in dynamodb tables in real time
	- can be read by
		- EC2
		- Lambda
		- ...
	- 24h retention of data
- Global Tables
	- cross region replication
		- a change made in a region is replicated to another region
	- active replication
	- many regions
	- must enable dynamodb stream
	- Cases
		- low latency
		- [[Disaster Recovery]]

## [[AWS Kinesis]] Data Stream for DynamoDB Stream
- Stream DynamoDB item changes to kinesis
- Longer retention periods (> 24h)

![[Pasted image 20220416145315.png]]

## DAX - DynamoDB Accelerator
- Seamless cache for DynamoDB
- No need to refactor code
- Writes goes through DAX to DynamoDB
- Micro Second for cached queries and items
- Solves the [[#Hot Key Problema]] (too many reads)
- 5min TTL default
- up to 10 nodes in the cluster
- Multi AZ
- Secure
	- Encryptiuon at rest with [[AWS KMS]]
	- VPC
	- IAM
	- CloudTrail