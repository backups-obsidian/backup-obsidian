---
created: 2022-04-18 18:50
updated: 2022-04-24 11:58
---
---
**Links**: [[../100 home]]

---

[[Introduction]]

## IAM
[[IAM Basics]]
[[STS & Identity Federation]]
[[Directory Services]]
[[Organisations]]
[[Miscellaneous]]
- **Random**
	- We can make calls to IAM using SDK or CLI but we can also make *direct calls to IAM web service* using the **Query API**(not recommended by AWS).
	- There shouldn't be an **explicit deny**.

## EC2
[[EC2 Basics]]
[[EC2 Instance Purchasing Options]]
[[EC2 Spot Instances & Fleet]]
[[EC2 Placement Groups]]
[[EC2 ENI]]
[[EC2 Hibernate]]
[[EC2 EBS]]
[[EFS]]
[[Instance store]]
[[EC2 AMI]]
[[EC2 Metadata]]
[[EC2 Lifecycle states]]

## ASGs
- Meaning of *horizontal scaling* and *high availability*
	- **Horizontal scaling** implies **distributed systems**. This is very common for web applications.
	- **High availability** means running your applications in **at least 2 AZs**. So one data centre failure doesn’t affect your business.
[[ASG]]
[[Scaling Policies]]
[[Termination Policy & Life Cycle Hooks]]
[[Launch Configuration-Template]]

## ELBs
[[ELB]]
[[Types of ELBs]]
[[Stickiness, Cross zone balancing & Connection Draining]]

## Databases
[[RDS]]
[[RDS Read Replica & Multi AZ]]
[[RDS Security]]
[[Aurora]]
[[ElastiCache]]
[[DynamoDB]]
[[Other Databases]]

## Route53
[[Route53]]
[[Route53 Routing Policies]]
[[Route53 Health Checks]]

## S3
[[S3]]
[[S3 Encryption]]
[[S3 Websites]]
[[S3 Replication]]
[[S3 Storage Classes]]
[[S3 Lifecycle Rules]]
[[S3 Performance]]
[[S3 Miscellaneous]]

## CloudFront & Global Accelerator
[[CloudFront]]
[[CloudFront Advanced]]
[[Global Accelerator]]

## AWS Storage

## Decoupling Applications
## Serverless
## Encryption
[[KMS]]

## Monitoring and Auditing
[[Cloud Trail]]


---
## Miscellaneous
- Billing is a **global** service.
- All the snapshots are stored in S3.

---
Later
- In S3 for **bucket level** permissions you **don't need trailing \*** in the resource like ListBucket. You need a **trailing \* for object level permissions** like get put or delete object.