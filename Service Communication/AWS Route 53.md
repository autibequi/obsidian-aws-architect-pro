# AWS Route 53

```toc
```
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
### Simple
- Route to a single resource
- Can't be associated with health checks
- Can specify multiple resources to the same record
	- **Will randomly select on by the CLIENT**
### Weighted
- Controle the % of the request that go to each resource
- Can be associated with Health Checks
- Use cases:
	- Load Balance between regions
	- Testing new app version
### Latency-Based
- Redirect to the resource that has the least latency
- **Latency is based on traffic between users and AWS Regions**
- Can be associated with health checks
### Failover
- if health check fails failover to another resource
### Geolocation
- Routing is based on user location
	- Country
	- Continent
	- US State
- Should create a "default" record for no match
	- Use cases
		- Website localization
		- restrict content distribution
		- load balancing
	- Can be associated with health checks
### Geoproximity
- Route based on geographic location from resource location (latitude longitude)
- Can define `bias` to shift more or less traffic to resources
	- To expand (1 to 99) - more traffic
	- To shrink (-1 to -99) - less traffic
- Resources can be:
	- AWS Resources
		- will use region as lat/long
	- Non-AWS Resources
		- must specify lat/long
- You must use [[AWS Route 53#Traffic Flow]]

### Multi-Value
- Use when routing traffic to multiple resources
- Route 53 returns multiple values/resources 
- Can be associated with Health Checks
	- Only returning the healthy ones
- Up to 8 healthy records are returned for each query
- **not a substitute for having an ELB**

## Traffic Flow
- Simplify the process of creating and maintaing records in large and complex configurations
- Visual editor
- Configurations can be saved as **Traffic Flow Policy**
	- supports versioning
	- can be applied to different [[AWS Route 53#Hosted Zones]]
	- 

## Hosted Zones
- Container for records that define how to route traffic
- Public Hosted Zones
	- Specify how to route traffic on the internet (public domain names)
- Private Hosted Zones
	- Specify how to route traffic whitin  one or more VPCs (private domain names)
	- must enable the VPC setting `enableDnsHostnames` and `enableDnsSupport`

## DNS Security Extension (DNSSEC)
- protocol for scuring DNS traffic
- verifies DNS data integrity and origin
- Protects agains man in the middle (MITM) attacks
-  Only works with Public Hosted Zones

## Health Checks
- HTTP Health Checks are for only **public resources**
- Automated DNS Failover
	- Checks endpoint
		- application
		- server
		- other aws resource
	- Calculated Health Checks
		- Combine health checks in a single one
		- can use OR AND NOT
		- upto 256 child health checks
		- specify minimal limit to pass
	- [[CloudWatch Alarms]]
- **Health Checks can be setup to pass/fail based on the text in the first 5120bytes of the response**

## Health Checks - Private Hosted Zones
- Route 53 health checkers are public 
	- outside the VPCs
	- cant access private endpoints
- Create a [[CloudWatch Metrics]] and associate a [[CloudWatch Alarms]] then create a health check that check this allarm.

## Hybrid DNS
- By default, route 53 resolver automatically answer DNS quereis for
	- Local domain names for EC2 instances
	- Records in Private Hosted Zones
	- Records in public Name Server
- Hybrid
	- Resolve DNS queries between VPC (Route 53 resolvers) and your networks (other DNS Resolvers)
	- networks can be
		- VPC / Peered VPC
		- On-Premises Network
			- Conected through
				- Direct Connect
				- AWS VPN

## Resolver Endpoints
- Inbound Endpoint
	- DNS Resolvers can foward DNS queries to R53
	- Allow you DNS Resolver to resolve domains for AWS Resources
- Outbound Endpoints
	- Route 53 Resolver fowards DNS queries to another DNS Resolver
	- Use **Resolver Rules** to foward DNS queries
- ASsociate with one or more VPCs on same Region
- Create in tow AZs for high availability
- Each endpoint supports 10.000 queries per second per IP address 

## Resolver Rules
- Controls which DNS queries are forwarded to other DNS
- Conditional Forwarding Rules
	- Forwards the resolve of a specific domain and subdomains to a **target ip address**
- System Rules
	- Override Forwarding Rules
- Auto-defined System Rules
	- Defines how DNS queries for selected domains are resolved
	- AWS internal domain names
	- Privated Hosted Zones #focus 