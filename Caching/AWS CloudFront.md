# AWS Cloud Front
```toc
```
---
- Content Delivery Network (CDN)
- Improves read performance
- Content is cached at [[AWS CloudFront#Edge Locations]]
- DDoS Protection
- Integration with
	- [[AWS Shield]]
	- [[AWS Web Application Firewall]]
- Can expose external HTTPS
- Can talk to internal HTTPS backends
- Origins
	- [[AWS S3]] Bucket
		- For file distribution
		- Enhance secrity with CloudFront [[Origin Access Identitiy]] (OAI)
		- CloudFront can be used as an ingress (to upload files to s3)
	- [[AWS S3]] Bucket as a Website Server
		- Enable `Static Website Hosting` on the bucket
	- MediaStore Container & MediaPackage endpoint
		- Deliver Video On Demand
		- Live Streaming videos using [[AWS Media Services]]
	- Custom Origin (HTTP)
		- EC2 Instance
		- [[Application Load Balancer]]
		- [[Classic Load Balancer]]
		- [[AWS API Gateway]]
		- Any HTTP backend you want 

## Edge Locations

## CloudFront vs [[AWS S3]] Cross Region Replication
- CloudFront
	- Global Edge Network
	- Files are cache for a TTL
	- Great for static content that must be available everywhere
- S3 Cross Region Replication
	- Must setup for each Reagion
	- Files are updated in nearin real-time
	- Read-Only
	- Great for dynamic content that needs to be available at low latency in few regions

## Geo Restriction
- Restrict who can access you distribution via
	- Allow List
	- Block List
- The `country` is determined using a third party GEO-IP Database
- Use case
	- Enforce Copyright Laws

## Signed URL
![[Pasted image 20220415225559.png]]

## CloudFront Signed URL vs [[AWS S3]] Pre-Signed URL
- CloudFront Signed URL
	- Allow access to a path, no matter the origin
	- Account wide key-pair
	- Only the root can manage it
	- Can filter by
		- IP
		- Path
		- date
		- Expiration
	- Can leverage caching features
- S3 Pre-Signed URL
	- Issue a request as the person who presigned the URL
	- Uses the IAM key of the signing IAM Principal
	- Limited Lifetime

## Restrict Access to [[Application Load Balancer]] and Custom Origins
- Prevent direct access to your ALB or Custom Origins
- Only Access via CloudFront
- Steps
	- Configure CloudFront to add a [[Custom HTTP Header]] to request sent to the ALB
	- Configure the ALB to only forward requests that contains that [[Custom HTTP Header]]
	- Must keep the custom header name as a secret!

## Caching
- Based on
	- Headers
	- Session Cookies
	- Query String Parameters
- The cache lives at each [[AWS CloudFront#Edge Locations]]
- You must maximize the cache hit rate to minimize request to the Origin
- Control TTL via Headers: `Cache-Control` and `Expires`
- Maximize cache hits by separating static and dynamic distributions

### Whitelist Headers
- Selects which headers will be used to match a cache

## CloudFront Caching vs [[AWS API Gateway]] Caching 
#doubt 
https://www.udemy.com/course/aws-solutions-architect-professional/learn/lecture/18376528

# Edge Manipulation
## CloudFront Functions
- Lightweight functions
- Written in JavaScript
- For high-scale, latency-sensitive CDN customizations
- Sub-ms startup
- Millions of request/sec
- Runs at Edge Locations
- Process Isolation #doubt 
- Edge Function
	- A code you write and attach to CloudFront Distributions
	- Runs close to client to minimize latency
	- No cache
	- Only change req/res
	- Two types
		- [[#CloudFront Functions]]
		- [[#Lambda@Edge]]
- Use Cases
	- Manipulate HTTP req/res
	- Implement filtering before reaching application
	- Authentication
	- Authorization
	- Generate HTTP response at the edge
	- A/B Testing
	- Bot mitigation
- No Servers
- Globally
- Cases
	- Change client request response between 
		- Cloudfront and Client
	- Cache Key Normalization
		- Transform req attributes
			- Headers
			- Cookies
			- Query Strings
			- URL
		- Optimize Cache Key Hit
	- Headers manipulation
	- URL rewrite or redirects
	- Auth
- Native feature of CloudFront
- Management entirely on CloudFront

## Lambda@Edge
- Uses [[AWS Lambda]]
- Made in
	- NodejS
	- Python
- Scales to 1000s req/res
- Runs at the nearest Regional Edge Cache
- VM-based isolation #doubt 
- Cases
	- Change request/response between 
		- Cloudfront and Client
		- Cloudfront and Origin
	- If you need 
		- libraries or SDKs
		- Network access to external services
		- File System access
		- Access to the body of the HTTP request
		- Longer execution than [[#CloudFront Functions]]
		- Adjustable CPU and Memory
- Creates the lambda function in one location
	- CloudFront replicate to the other locations for you

## CloudFront Functions vs Lambda@Edge
![[Pasted image 20220416130356.png]]
### CloudFront Functions with Lambd@Edge
![[Pasted image 20220416130101.png]]
### Lambda@Edge Only
![[Pasted image 20220416130250.png]]

# HTTPS configuration and Host #focus 
![[Pasted image 20220416131344.png]]

