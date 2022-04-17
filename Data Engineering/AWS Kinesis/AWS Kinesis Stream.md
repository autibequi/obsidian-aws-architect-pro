# AWS Kinesis Streams

- Divided in ordered shards/partitions
- Data retention
	- 24h default
	- up to 365 days
- Ability to repocess/replay data
	- last 24h
	- up to 7 days
- Mulitple aplications can consume the same stream
- Once information is added to Kinesis it **cannot be deleted** (immutability)

## Kinesis Streams Shards
- on-demand
	- no capacity planning
	- Kinesis scales shards  automatically
- Provissioned
	- You manage the shard over time
- Batching available
- or per message
- The number of shard evolve over time
	- reshard
	- merge
- records are ordered by shards

## Kinesis Consumer & Producers
- Producers
	- AWS SDK
	- Kinesis Producer Library
		- JAVA
		- C++
		- retries
		- compression
		- batch
	- Kinesis Agent
		- Monitor logs
		- Can write to
			- [[AWS Kinesis Stream]]
			- [[AWS Kinesis Firehose]]
- Consumers
	- SDK
	- Lambda
		- via [[Event Source Mapping]]
	- KCL - Kinesis Client Library #focus 
		- Checkpointing
		- Coordinated reads

## Limits
- Producers
	- 1 MB/s or 1000messages/s **PER SHARD**
		- if exceeded => `ProvisionedThroughputException`
- Consumer
	- Classic
		- 2MB/s **PER SHARD** accross all consumers
		- 5 API calls per second **PER SHARD**  across all consumers
	- Enhanced Fan-Out
		- 2MB/s **PER SHARD**, **PER ENHANCED CONSUMER**
		- No API calls needed (push model)
- Data Retention
	- 24h default
	- Extendeable to 7 days