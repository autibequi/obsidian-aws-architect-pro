# Network Load Balancer (v2)
- Layer 4
	- Foward TCP & UDP traffic to your instances
	- Handle millions of requests/sec
	- Less latency ( ~100ms vs 400ms for [[Application Load Balancer]])
- has **one static IP per AZ**
- supports assigning [[Elastic IP]]
	- helpful for whitelisting specific IP
- used for extreme performance, TCP or UDP
- No free tier

## Target Groups
- EC2 instances
- IP Address - Must be private IP
- [[Application Load Balancer]]
	- Example:
		- keep static IP
		- keep layer 7 path routing from ALB