# AWS FSx
- Launch third party high-performance file system on AWS
- Fully Managed

## FSx for Windows
- File System share drive
- support 
	- [[SAMBA]] protocol
	- Windows NTFS
- Microsoft AD integration
- ACLs
- User Quotas
- Can be mounted on Linux
- Scales
	- Up to 10s of GB/s
	- millions of IOPs
	- 100s PB of data
- Storage Options
	- SSD - Latency sensitive
	- HDD - slower, less expnsive
- Can be access from your on-premise infra
	- via VPN or Direct Connect
- Can have MultiAZ
- Data is backed up daily to S3

## FSx for Lustre
- Lustre is a type of parallel distributed file system
- for lasrge scale computing
- Lustre = Linux + Cluster
- Cases
	- Machine Learning
	- [[High Peformance Computing]]
	- Video Processing
	- Financial Modeling
	- Eletronic Desgin Automation
- Scales
	- Up to 10s of GB/s
	- millions of IOPs
	- 100s PB of data
- Storage Options
	- SSD - Latency sensitive
	- HDD - slower, less expnsive
- Seamless integration with s3
	- Can read S3 files as a File System
	- Can write the output of the computation back to S3
- Can be access from your on-premise infra
	- via VPN or Direct Connect

## FSx File System Deployment Options
- Scratch File System
	- Temporary Storage
	- Data is not replicated 
	- high burst 
		- 6x fasetr
		- 200MBps per TiB
	- Cases
		- short-term processing
		- optimize costs
- Persistent File System
	- LongTerm Storage
	- Data is replicated within same AZ
	- Replace failed files within minutes
	- Usage:
		- Longe-term processing
		- sensitive data
		- 