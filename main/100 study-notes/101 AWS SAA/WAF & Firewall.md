---
created: 2022-04-29 10:03
updated: 2022-04-29 10:15
---
---
**Links**: [[101 AWS SAA Index]]

---
## WAF
- Protects our *web applications* from common **web exploits (layer 7 - HTTP)**
- It can be deployed on **3** things: 
	- **ALB** 
	- **API Gateway**  
	- **CloudFront**

- To use WAF we *must define WACL* (web access control lists).
- In WACL there can be **rules on different things**. There can be rules on **IP addresses**, HTTP Headers, HTTP body or URI strings
	- We can *block countries* using the **geo-match** feature or allow/block only certain IPs.
	- We can also apply some **Rate Based Rules for DDoS protection**. For example an IP should not do more than 5 requests per second.

- It can **protect from basic attacks** such as **SQL injection** and **XSS**

> [!caution] For DDoS you can either go for [[Shield]] or *Rate Based Rules of WAF*.

## Firewall
- Manage *rules of all accounts of an AWS organisation*. 
	- Like *centrally manage EC2 Security Groups* and AWS Shield Advanced across all AWS accounts in your AWS Organisation.

- What can we **manage** using firewall:
	- Common set of security rules
	- *WAF rules* (Application Load Balancer, API Gateways, CloudFront)
	- *AWS Shield Advanced* (ALB, CLB, Elastic IP, CloudFront)
	- *Security Groups* for EC2 and *ENI* resources in VPC
