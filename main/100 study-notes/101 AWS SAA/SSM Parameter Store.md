---
created: 2022-04-29 09:03
updated: 2022-04-29 09:13
---
---
**Links**: [[101 AWS SAA Index]]

---

- SSM stands for **Systems Manager**
- **Secure storage for configuration and secrets**.
- Optional encryption using KMS
- **Serverless**, scalable, durable with easy to use SDK.
- **Version tracking** for configuration and secrets.
- **Integration with CloudFormation**
- Configuration management *path* & *IAM*
	- ![[attachments/Pasted image 20220429090459.png]]

- *Notifications using CloudWatch events*. In [[Config]] we had notifications using either CloudWatch events or SNS.
- *Standard tier is free* whereas advanced tier is not.
- We *can inject sensitive data into ECS* using SSM parameter store and secrets manager.