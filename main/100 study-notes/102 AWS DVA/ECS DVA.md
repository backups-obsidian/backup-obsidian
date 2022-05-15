---
created: 2022-05-15 11:30
updated: 2022-05-15 13:10
---
---
**Links**: [[102 AWS DVA Index]]
**Recommended Reads**: [[../101 AWS SAA/ECS | ECS]]

---
## ECS Tasks and Services 
- When we create an ECS cluster we specify the *launch types* (by default fargate is selected), VPC and subnets to be used.
- Task Definition indicates how to create an ECS task.
- To create a service we should first create a task definition.
- We get 20 GBs of ephemeral storage from Fargate.
- If we are creating an *ECS Service we will need an ALB to balance the ECS tasks*.
	- We will need 2 SGs. One for ALB and other for ECS tasks.
- *ECS tasks can be invoked by EventBridge*. 
	- We can use them *over Lambdas* if the required execution time is more than 15 mins.
	- ![[attachments/Pasted image 20220515130441.png]]

> [!tip]- If you want to launch a group of tasks then use a service. If you want to run a single task then go with simple task configuration.
> In case of ECS tasks you won't get an option to use load balancing
> ---
> ![[attachments/Pasted image 20220515123458.png]]

### Autoscaling
- We can manually increase or decrease the desired number of ECS tasks in a service. But this can also be done **automatically using AWS Application Auto Scaling**.
- We can scale on 3 metrics
	- ECS Service *Average CPU Utilisation*
	- ECS Service *Average Memory Utilisation* (RAM)
	- *ALB Request Count Per Target* metric coming from the ALB

- We can also use scaling methods like Target Tracking, Step Scaling, Scheduled Scaling.
- Fargate autoscaling is much easier to scale.

#### EC2 Launch Type - Auto Scaling EC2 Instances
- Accommodate ECS Service Scaling by adding underlying EC2 Instances
- Auto Scaling Group Scaling
	- Scale your ASG based on CPU Utilisation
	- Add EC2 instances over time
- ECS Cluster Capacity Provider (Recommended and easier)
	- Used to *automatically provision and scale the infrastructure* for your ECS Tasks
	- Capacity Provider *paired with an Auto Scaling Group*
	- Add EC2 Instances when you're missing capacity (CPU, RAM etc)

> [!tip] If you are using *EC2 Launch Type* then use *ECS Cluster Capacity Provider* to scale the EC2 instances.

## ECS Task Definitions