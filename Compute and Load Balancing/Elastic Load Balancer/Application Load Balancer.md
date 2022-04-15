# Application Load Balancer (v2)
- [[ISO Model#Layer 7]]
- Load Balance multiple HTTP apps 
	- accross [[Target Groups]]
	- same machine
		- greate fit  [[Elastic Container Service#Dynamic Port Mapping]]
- Supports HTTP/2 and WebSocket
- Support Reddirects (http -> https for example)
- Routing Rules for
	- paths
	- headers
	- query string

## Target Groups
- EC2 Instances (can be managed by [[Auto Scaling#Auto Scaling Groups]])
- [[Elastic Container Service#Task Definitions]]
- [[AWS Lambda]]
- IP Addresses
	- Must be private IPs
- [[Application Load Balancer]] Can Route to multiple Targets
- Health Checks are at the target group level