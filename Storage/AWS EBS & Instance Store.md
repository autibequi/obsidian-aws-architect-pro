# EBS - Elastic Block Storage
- Network drive you attach to **ONE** instance only
- Linked to specific AZ
	- To transfer you need to snapshot then restore in another AZ
- Volumes can be resized
- Need to be used in a [[EBS Optimized]] Instance Type for maximum throughput.

## Volume Types #focus 
| name                      | type | description                                                    |
| ------------------------- | ---- | -------------------------------------------------------------- |
| gp2/gp3                   | SSD  | General purpose SSD                                            |
| io1/io2/io2 Block Express | SSD  | Highest-Performance SSD, low latency, high-throughput workload |
| st1                       | HDD  | Low cost, frequently accessed, throughput instensive workloads |
| sc1                       | HDD  | lowest cost HDD, less frequently accessed workloads            |
 
- EBS are characterized in
	- Size
	- Throughput
	- IOPS
- Can be used as boot volumes
	- gp2/gp3
	- io1/io2

## Snapshot
- Incremental 
	- Only backup changed blocks
- EBS backups uses IO
	- Avoid doing while in high demand
- Saved on S3 
	- But you can't see them
- Not necessary to detach volume, but recommended
- Can copy snapshots accross regions for [[Disaster Recovery]]
- Can make [[AMI]] Images from Snapshots
- Restored EBS Volumes need to be pre-warmed for maximum performance
	- Use `Fast Snapshot Restore`(FSR) feature 
	- Or fio/dd command to read the entire volume

## EBS Multi-Attach 
- IO1/IO2 family only
- Attach the same EBS volume to multiple Instances in the same AZ
- Full Access to all Instance
- Use Case
	- Achieve Higher Application Availability in clustered Linux Applications
	- Application must manage concurrent write operations
- Must use a file system that's cluster-aware
	- Not XFS, EX4, etc

## Local EC2 Instance Store
- Physical disk attached to the physical server where your Instance is
- Very high IOPS
- Disks up to 7.5 TiB
- Block Storage (like EBS)
- RIsk of data loss if hardware fails
- Cannot be Increased in Size

## Instance Store vs EBS
- Instance Store is 
	- physical ly attached
	- ephemeral storage
	- beter I/O performance (more IOPS)
	- Good for cache/buffer/scratch data/temporary content
	- Data survives reboot
	- On stop/terminate the instance is lost
	- You can't resize
	- Backups must be operated by the user
- EBS is 
	- a network drive 
	- persistent
