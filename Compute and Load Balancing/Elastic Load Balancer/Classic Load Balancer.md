# Classic Load Balancer (v1)
- HealthCheck can be HTTP or TCP inclusding SSL
- Supports only one SSL certificate
	- SSL Certificate can have many [[Multi-Domain Certificates#Multi-Domain Certificates]] (SAN)
	- Needs to update if SAN is add/edit/remove
	- Better use ALB with SNI (Server Name Indication)
		- Use many SSL Certificate in the Load Balancer 