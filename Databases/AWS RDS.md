# AWS RDS - Relational Database Service
- Engines
	- PostegreSQL
	- MariaDB
	- MySQL
	- Oracle
	- SQL Server
- Managed Database
	- provisioning
	- backup
	- patching
	- monitoring
- Launch withing a VPC
- Storage based on [[AWS EBS]]
	- gp2 
	- io1
	- Can increase size automatically with autoscaling 
- Backups
	- automatically
	- point in time recovery
	- backups expires
- Snapshots
	- manual
	- can be used to make copies across regions
- Events
	- via SNS
- Multi AZ
	- Sync Replication
	- Automatically
	- Via DNS 
	- For Disaster Recovery
- Read Replica
	- Async Replication
		- Eventual Consistency
	- For increase read throughput
	- Can be Cross-Region

## Security
- KMS Encryption at rest for EBS volume/snapshot
- Transparent data ecnryption #focus for oracle and SQLserver
- SSL Encryption to RDS is possible for all DB (inflight)
- IAM Authentication for mysql and postgresql
- authorization still happens withing rds (no in IAM)
- Cloudtrail cannot be used to track queries from RDS databases
- Can create a encrypted RDS snaptshot to a encrypted one

## Oracle - Exam Tips
- Backups
	- Use RDS backup & Restore
		- When RDS for Oracle
		- Can be used to create another RDS Oracle DB
	- Use ORMAN (Oracle Recovery Manager)
		- For non-RDS Oracle Databases
		- Creates a Backup that can be used to make a EC2 Instance DB
- Supports
	- TDE - Transfer Data Encryption
		- Encrypts data before saving on storage
	- [[AWS DMS]] #focus 
- RAC
	- No RDS Support
	- Only works on Oracle DB running on Ec2

## MySQL - Exam Tips
- Use mysqldump to migrate to non RDS databases

## RDS Proxy for [[AWS Lambda]]
- Avoid Too Many Connections from many Lambda Executins Running
- No need to code to clean up
- IAM Authentication
- DB Authentication

![[Pasted image 20220416165532.png]]


