# AWS Elastic Cache
- Managed Instances of
	- Redis
	- Memcahed
- AWS takes care of
	- OS Maintenance
	- Patching
	- Optimizations
	- setup
	- confguration
	- monitoring
	- failure recovery
	- backups
- Requires code to use the cache

## Redis vs Memcached
- Redis
	- Muli AZ
	- Auto Failover
	- Read Replicas 
		- Scales 
		- High Available
	- Persistent
	- Data Durability
	- Read Only File Feature (AOF) #doubt 
	- Backup and Restore feature
- MemCached
	- MultiNode for patitioning (sharding)
	- non persistent
	- no backup and restore
	- multi-threaded architecture