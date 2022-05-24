---
created: 2022-05-24 10:24
updated: 2022-05-24 11:03
---
---
**Links**: [[102 AWS DVA Index]]

---
## Environment Variables
- Environment variable = *key/value pair* in **String form**
- Adjust the function behaviour without updating code
- The environment variables are available to your code
- Lambda Service adds its own system environment variables as well
- Helpful to store **secrets** (*encrypted by KMS*)
	- Secrets can be encrypted by the *Lambda service key, or your own CMK*

## Logging & Tracing
- **CloudWatch Logs**:
	- AWS *Lambda execution logs are stored in AWS CloudWatch Logs*
	- Make sure your AWS Lambda function has an execution role with an IAM policy that authorises writes to Cloud Watch Logs

- **CloudWatch Metrics**: 
	- AWS Lambda *metrics* are displayed in AWS Cloud Watch Metrics
	- *Invocations*, Durations, *Concurrent Executions*
	- *Error count*, *Success Rates*, *Throttles*
	- *Async Delivery Failures*
	- Iterator Age (Kinesis & DynamoDB Streams)

## Tracing
- Enable in Lambda configuration (*Active Tracing*)
- *Runs the X-Ray daemon* for you
- Use AWS **X-Ray SDK in Code**
- Ensure *Lambda Function has a correct IAM Execution Role*
	- The managed policy is called `AWSXRayDaemonWriteAccess`
- *Environment variables* to **communicate with X-Ray**
	- `_XAMZN_TRACE_ID`: contains the tracing header
	- `AWS_XRAY_CONTEXT_MISSING`: by default, LOG_ERROR
	- `AWS_XRAY_DAEMON_ADDRESS`: the *X-Ray Daemon IP_ADDRESS:PORT*

## Lambda in VPC
### Default VPC
- By **default**, your Lambda function is launched **outside your own VPC** (in an *AWS-owned VPC*)
- Therefore it **cannot access resources in your VPC** (RDS, ElastiCache, internal ELB, etc)
	- ![[attachments/Pasted image 20220524104326.png]]

### Our VPC
- To *deploy lambda in our VPC*:
	- You must define the *VPC ID*, the *Subnets* and the *Security Groups*
	- **Lambda will create an ENI** (Elastic Network Interface) in your subnets
	- `AWSLambdaVPCAccessExecutionRole` is required.
	- ![[attachments/Pasted image 20220524110228.png]]
- Example: 
	- ![[attachments/Pasted image 20220524104601.png]]
	- In the above example *RDS security group must allow access from the security group of Lambda*.

#### Internet Access
- A **Lambda function in our VPC does not have internet access**

> [!caution]- Deploying a Lambda function in a *public subnet* (which has internet access)  *does not give it internet access or a public IP*
> Instead in **needs to be deployed in a private subnet and use NAT Gateway in public subnet for internet access**.
> ![[attachments/Pasted image 20220524105942.png]]

- Deploying a Lambda function in a *private subnet* gives it internet access **if you have a NAT Gateway/Instance**.
	- You can use *VPC endpoints to privately access AWS services* without a NAT. Like DynamoDB
	- ![[attachments/Pasted image 20220524105007.png]]

> [!note]- Lambda *CloudWatch Logs works even without endpoint or NAT Gateway*
- Also read [[../101 AWS SAA/Lambda#Using our own VPC|using our own vpc]].

