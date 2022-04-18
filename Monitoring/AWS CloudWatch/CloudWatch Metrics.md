# AWS Metric
- Provided by many AWS services
- EC2 
	- Standart
		- 5min
	- Detailed Monitoring
		- 1min
	- No RAM metric out-of-the-box
- Custom Metrics
	- Standar Resolution
		- 1min
	- High Resolution
		- 1 sec
## Filters & Insights
- [[CloudWatch Logs]] can be used to filter expressions
	- exemple
		- find an id
		- count amount of string "ERRORS"
	- Cam be used tot rigger allarms