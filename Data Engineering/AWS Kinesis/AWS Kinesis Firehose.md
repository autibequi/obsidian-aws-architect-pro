# AWS Kinesis Firehose
![[Pasted image 20220417132545.png]]

- Fully Managed
- Serverless
- Automaticaly Scale 
- Pay only for that going thought Firehose
- Near RealTime
	- Not real time because writes in batches
	- 60 sec minimium for non full batches #doubt 
	- or minimium 1MB at a time
- Supports
	- Many data formats
	- conversions
	- transformations
		- Custom transformation via [[AWS Lambda]]
	- compression
- Send all data (or only failed to write data) to [[AWS S3]]

## Firehose Buffer Sizing
- Acumulates records in a buffer
- buffer is flushed based on
	- Time
	- Size Rules
		- User Defined
		- Can automatically increase to increase throughput
- **If you need real time flush to [[AWS S3]] use [[AWS Lambda]]
	- Will be more expensive

## [[AWS Kinesis Stream]] vs [[AWS Kinesis Firehose]]
![[Pasted image 20220417134048.png]]
- 