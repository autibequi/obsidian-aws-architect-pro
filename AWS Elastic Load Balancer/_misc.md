# Misc
## Sticky Session or Session Affinity
- Same client is always redirected to the same instance behind a load balancer
- Available for
	- [[Application Load Balancer]]
	- [[Classic Load Balancer]]
- Cookie used for stickiness has expiration date you control
-  May cause inbalance to the load over the EC2 Instances

## Request Routing Algorithms
### Least Outstanding Requests
- The next instance to receive the request is the one with the lowest number of pending/unfinished requests
- Works on (HTTP)
	- [[Application Load Balancer]]
	- [[Classic Load Balancer]]

### Roud Robin
- Equally choose the targets from the target group
- Works on (TCP)
	- [[Application Load Balancer]]
	- [[Classic Load Balancer]]

### Flow Hash #focus 
- Selects a target based on a hash created using:
	- protocol
	- source/destination ip address
	- source/destination port
	- TCP Sequence number
- Each TCP/UDP connection is routed to a single target for the life of the connection
- Works on
	- [[Network Load Balancer]]
