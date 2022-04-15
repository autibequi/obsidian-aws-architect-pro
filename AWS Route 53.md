# AWS Route 53

## Record Types
- A
	- maps a hostname to IPV4
- AAAA
	- maps a hostname to IPV6
- CNAME
	- maps a hostname to another hostname
	- the target must have an A or AAAA record
	- can't create CNAME record for the top node of a DNS namespace ([[Zone Apex]])
		- Example
			- Can't create for example.com 
			- But can create for www.example.com
- NS
	- Name Server for the Hosted zone
	- Control how traffic is routed for a domain

## CNAME vs Alias
- AWS Resources expose an AWS Hostname
- CNAME
	- Points Custom Hostname to an AWS hostname
		- Example:
			- us-east-2.elb.amazonaws.com => www.example.com
	- **ONLY FOR NON ROOT DOMAINS**
- Alias
	- Points a custom hostname to an AWS Resource
	- Can be used for root domains or non-root domains
	- Free of charge
	- Native health check

## Alias
- Records Targets
	- Elastic Load Balancers
	- [[AWS CloudFront]]
	- [[AWS API Gateway]]
	- [[Elastic Beanstalk]] Env
	- S3 Website
	- VPC Interface Endpoints
	- [[AWS Global Accelerator]]
	- [[AWS Route 53]] record in the same hosted zone
	- [[AWS EC2]] DNS name

## Record TTL
- High TTL
	- Cheaper
	- possibly outdated records
- Low TTL
	- Expensive
	- Records are outdated for less time
- Mantatory for all Records
	- Except ALIAS Records

## Routing Policies
- Simple
	- Route to a single resource
	- Can't be associated with health checks
	- Can specify multiple resources to the same record
		- **Will randomly select on by the CLIENT**
- Weighted
	- Controle the % of the request that go to each resource
	- Can be associated with Health Checks
	- Use cases:
		- Load Balance between regions
		- Testing new app version
- Latency
	- Redirect to the resource that has the least latency
	- **Latency is based on traffic between users and AWS Regions**
	- Can be associated with health checks
- 
