---
created: 2022-04-17 15:43
updated: 2022-05-24 11:06
---
---
**Links**: [[../100 home | 100 Home]]
**Recommended Reads**: [[../101 AWS SAA/101 AWS SAA Index | AWS SAA Index]]

---
## Databases
[[ElastiCache DVA]]
[[ElasticCache Replication]]

## Extra
[[CLI]]
[[AWS Limits]]
[[CloudFront DVA]]
[[ECS DVA]]

## ElasticBeanstalk
[[ElasticBeanstalk DVA]]
[[ElasticBeanstalk Deployment Modes]]
[[ElasticBeanstalk Docker]]

## CI/CD
- Tech Stack
	- ![[attachments/Pasted image 20220516161339.png]]

[[CodeCommit]]
[[CodePipeline]]
[[CodeBuild]]
[[CodeDeploy]]
[[CodeStar]]
[[CodeArtifact]]
[[CodeGuru]]

## CloudFormation
[[CloudFormation]]
[[CloudFormation Template Components]]
[[CloudFormation Intrinsic Functions]]
[[CloudFormation RollBacks]]
[[CloudFormation Advanced]]

## Monitoring, Troubleshooting & Auditing
- AWS CloudWatch offer us: 
	- *Metrics*: Collect and track key metrics
	- *Logs*: Collect, monitor, analyse and store log files
	- *Events*: Send notifications when certain events happen in your AWS. Recommended to use EventBridge.
	- *Alarms*: React in real-time to metrics/events

[[../101 AWS SAA/CloudWatch | CloudWatch]]
[[../101 AWS SAA/EventBridge | EventBridge]]
[[X-Ray]]
[[X-Ray Advanced]]
[[../101 AWS SAA/CloudTrail | CloudTrail]]

## Messaging: SQS, SNS & Kinesis
[[../101 AWS SAA/SQS | SQS]]
[[SQS DVA]]
[[../101 AWS SAA/SNS | SNS]]
[[../101 AWS SAA/Kinesis | Kinesis]]
[[Kinesis DVA]]

## Lambda
[[../101 AWS SAA/Lambda | Lambda]]

Three ways in which Lambda processes events
- [[Lambda Synchronous Invocation]]
- [[Lambda Asynchronous Invocation]]
- [[Lambda Event Source Mapping]]

[[Lambda Destinations]]
[[Lambda IAM Role]]
[[Lambda Configuration & Deployments]]
[[Lambda Performance]]

### Miscellaneous
- For *logging*:
	- For *each lambda a log group* is created. 
	- The logs are then grouped into streams. We can find the logs if we go inside a particular stream.

## Miscellaneous
- Typical 3 tier architecture
	- ![[attachments/Pasted image 20220514121352.png]]
	- *Data subnet* is also a *private subnet*.
