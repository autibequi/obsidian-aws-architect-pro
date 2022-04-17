# AWS Kinesis
- Managed "Data Streaming" Service
- Great for
	- Logs
	- metrics
	- IoT
	- clickstreams
	- real-time big data app
	- Streaming Processing Framework
		- Spark
		- NiFI
		- etc
- Data is automaticaly replicated syncroniously to 3 AZ

![[Pasted image 20220416201639.png]]
- Composed of 3 Services
	- [[AWS Kinesis Stream]]
		- Low Latency streaming ingestion at scale
	- [[AWS Kinesis Data Analytic]]
		- real time analytics on streams using SQL
	- [[AWS Kinesis Firehose]]
		- Load streams into
			- [[AWS S3]]
			- [[AWS Redshift]]
			- [[Amazon OpenSearch]]
			- Splunk

## Comparsion Chart
![[Pasted image 20220417135545.png]]

## Kinesis Agent
- the kinesis agent can send to firehose directly