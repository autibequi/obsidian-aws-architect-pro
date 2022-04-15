# SSL Encryption
## Basics
- Secure Sockets Layer
	- encrypt connections
- Transport Layer Security
	- Newer SSL
	- Mostly used
	- people still call it SSL
- SSL Certificates are issued by Certificate Authorities (CA)
	- comod
	- symantec
	- godaddy
	- globalsign
	- digicert
	- letsencrypt
	- ...
- SSL Certificate have an expiration date

## How it Works
- Assyetric Encrypton is expensive
	- used only as handshake then exchange it for a symetrical key (cheaper to CPU)
![[Pasted image 20220414155602.png]]

## SSL - Server Name Indication (SNI)
- Solves the problem of loading multiple certificate onto on webserver (for multiple websites)
- "newer" protocol
- requires the client to indicate the hoistname of the target server in the initial SSL handshake
- The server will then find the correct certificate or return a default one
- Only works with
	- ALB - [[Application Load Balancer]]
	- NLB - [[Network Load Balancer]]
- Doens work
	- CLB - [[Classic Load Balancer]] (old gen)
- The load balancer will provide the correct ceritficate and redirect to the corret taget grup of that application

## SSL - Man in the Middle Attacks
![[Pasted image 20220414160402.png]]
- Avoid man in the middle
	- Use HTTPS
	- use DNS that has [[DNSSEC]] #focus 