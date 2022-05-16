---
created: 2022-05-16 16:54
updated: 2022-05-16 19:06
---
---
**Links**: [[102 AWS DVA Index]]

---
- **Source**: 
	- *CodeCommit* 
	- *S3* 
	- Bitbucket 
	- *GitHub*
- **Build instructions**: Code file `buildspec.yml` (at the **root** of the source code) or insert *manually in CodeBuild console*.
- *Output logs* can be stored in Amazon *S3* & *CloudWatch Logs*
- Use CloudWatch Metrics to monitor build statistics
- Use *CloudWatch Events to detect failed builds* and trigger notifications
- Use *CloudWatch Alarms to notify if you need thresholds* for failures
- **Build Projects can be defined within CodePipeline or CodeBuild**
- CodeBuild **uses containers** to run the environments.
- You can use a list of supported environments for building your code and if your environment is not there then you *can use docker*.
- CodeBuild can be run locally by using docker and CodeBuild Agent. This is good for troubleshooting beyond logs.

> [!important]+ By default CodeBuild containers are launched **outside VPC**.
> - We can specify a *VPC configuration*: **VPC ID**, **Subnet IDs**, **Security Group IDs**
> - Then your build can access resources in your VPC (e.g., RDS, ElastiCache, EC2, ALB, etc)
> - *Use cases*: integration tests, *data query*, *internal load balancers*, etc.

## How it works
![[attachments/Pasted image 20220516185423.png]]

## `buildspec.yml`
- Must be at the **root of the source code**.
- We can define *env variables* either in *plain text* or we can use either *SSM Parameter Store* or *Secrets Manager*.
- **phases**: specify **commands** to run. *install*, *pre_build*, *Build*, *post_build*.
- **artifacts**: what to *upload to S3* (encrypted with KMS)
- **cache**: files to cache (usually *dependencies*) to S3 for future *build speedup*
