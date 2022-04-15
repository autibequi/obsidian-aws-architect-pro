# CloudHSM
![[Pasted image 20220414153259.png]]
- AWS Provision encryption hardware
- Dedicated hardware (HSM = Hardware security module)
	- is tamper resistante
	- support both symetric and assymetric encryption
- no free tier aailable
- must use the cloudhdsm client software
- redshift supports cloudhsm for database encryption and key management
- You manage your own encrption keys entirely (not AWS)
- Good Option to use with [[SSE-C]] encryption
- Are spread across multiaz

# CloudHSM vs KMS
![[Pasted image 20220414161614.png]]![[Pasted image 20220414161621.png]]
## CloudHSM - SSL Offoading
- Offload ssl to cloudhsm (SSL Acceleration)
- supporte by 
	- nginx
	- apache
	- ISS for windows server
![[Pasted image 20220414161841.png]]