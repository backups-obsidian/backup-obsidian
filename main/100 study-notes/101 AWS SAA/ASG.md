---
created: 2022-04-20 19:15
updated: 2022-04-20 20:55
---
---
**Links**: [[101 AWS SAA Index]]

---

- Scale in removing, scale out adding.
- We can specify the **minimum**, **desired** and **maximum** number of EC2 instances running in an ASG. If desired == maximum then alarms won't add any new EC2 instances.
- We can *automatically register new instances to the load balancer*. ASGs and Load Balancers work hand in hand.
- To launch new instances we provide [[Launch Configuration-Template]]. In this launch configuration/template we provide details like AMI type, volume size etc.
- ASGs are free to use.

> [!caution] A role applied to ASG will be applied to all the EC2 instances in the ASG.

- Having instances under an ASG means that if for some reason they get terminated then ASG will automatically create new ones for replacement.

> [!info]- If EC2 instances are *marked unhealthy* by the load balancer then they are **terminated** by ASG and then relaunched.
> Instances are not restarted but terminated.

- We **can add running instances to an ASG**.

> [!important]- You *can edit ASGs* after they have been created but you *cannot edit launch configurations*. You *can edit launch templates*.
> So if you want your instances to use a new AMI and they are using launch configuration then you can just create a new launch configuration and update the ASG.

- While creating an ASG we have to specify the subnets. Make sure you specify all the subnets.

## Health Checks
- If *using an ELB* it is best to **enable ELB health checks** as otherwise *EC2 status checks may show an instance as being healthy that the ELB has determined is unhealthy*. In this case the *instance will be removed from service by the ELB but will not be terminated by Auto Scaling*.
-   By **default** uses **EC2 status checks**.
-   **Can also use ELB health checks and custom health checks**.
-   **ELB health checks are in addition to the EC2 status checks**.
-   If any health check returns an **unhealthy** status the **instance will be terminated**.
-   With ELB an instance is marked as *unhealthy* if ELB reports it as *OutOfService*
-   A *healthy* instance enters the *InService* state.
-   If connection draining is enabled, Auto Scaling waits for in-flight requests to complete or timeout before terminating instances.
-   **The health check grace period allows a period of time for a new instance to warm up before performing a health check (300 seconds by default**).

-  You can put an instance that is in the *InService* state into the *Standby* state, update some software or troubleshoot the instance, and then return the instance to service. Instances that are on standby are still part of the Auto Scaling group, but they do not actively handle application traffic.
- If the instance is in *Impaired status* Amazon EC2 Auto Scaling *does not immediately terminate instances*.

## Auto Scaling Alarms
- These alarms trigger scaling.
- We *can scale ASGs based on CloudWatch alarms*. We need 2 alarms, one for scaling in and other for scaling out. 
- A monitoring unit for CloudWatch alarms can be CPU usage. *Metrics are the **average** of all the ASG instances*.
- We can define *better auto scaling rules* that are **directly managed by EC2**. These rules are easier to set than the CloudWatch alarms. Some of these rules include average CPU usage, network in/out etc.
- We can also auto scale on a **custom metric** (ex no of connected users). We send the parameter of our custom metric to cloud watch alarms via the **PutMetric API**. Now we can create cloud watch alarms with this metric to scale in or out. So *ASG is not just limited to the metrics AWS exposes*.