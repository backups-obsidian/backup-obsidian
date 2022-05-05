---
created: 2022-04-19 16:22
updated: 2022-05-05 20:21
---
---
**Links**: [[101 AWS SAA Index]]

---
## Introduction
- It is a **fully managed**, **highly available** with **replication across multi AZs** database.
- It is a **NoSQL** database.
	- A SQL database has a rigid schema. Go for NoSQL databases if you need a flexible schema.
- It *scales to massive workloads*, distributed database.
- **Integrated with IAM for security**, authentication and authorisation.
- **Low cost** and **scales automatically**. 
	- By default, Auto Scaling is not enabled in a DynamoDB table which is created using the *AWS CLI*.
	- Autoscaling is *free of cost*. 

> [!question] The main differentiator will be keywords like "*scaling*" in questions. In *RDS, you still have to manually scale up your resources and create Read Replicas to improve scalability* while in DynamoDB, this is automatically done.

- DynamoDB is **made up of tables.** We **directly create tables** instead of creating databases.
- *Each table must* have a **Primary Key** which must be decided at creation time. **Combination** of the **partition key and the sort key** constitutes the primary key.
- Each table can have **infinite number of rows (items)**.
- Each row can have **columns (attributes)** which can be null.
- **Maximum size** of an **item (row)** is **400KB**.
	- Store *objects larger than 400KB in S3 and use pointers* in DynamoDB

- It allows us to write to *2 tables at the same time or to None* as part of one specific write.
- Store more frequently and less frequently accessed data in *separate tables*.
- **All DynamoDB tables are encrypted**. 
	- There is *no option to enable or disable encryption* for new or existing tables. 
	- By *default*, all tables are encrypted *under an AWS owned customer master key (CMK)* in the DynamoDB service account. 
	- However, you *can select* an option to encrypt some or all of your tables under a *customer-managed CMK* or the *AWS managed CMK* for DynamoDB in your account.

## Read and Write Capacity Modes
- *Control* how you manage your **table’s capacity** (*read/write throughput*)
- **Provisioned** Mode:  
	- **Default** 
	- You specify the number of reads and writes per second. This means capacity has to be planned before hand.
	- RCU and WCU can be increased independent of each other.
	- You pay for *provisioned Read Capacity Units (RCU)* & *Write Capacity Units (WCU)*
	- *Cheaper* as compared to on demand mode

- **On Demand** Mode:
	- Read/writes *automatically scale up/down* with your workloads
	- *No capacity planning needed*
	- Useful for **unpredictable** workloads 
	- It is **2x -3x more expensive** than the provisioned mode.

## DynamoDB Accelerator (DAX)
- **Fully-managed**, **highly available**,  **in memory cache** for DynamoDB. Helps solve read congestion by caching.
- **Doesn't** require **application logic modification.** Compatible with existing DynamoDB APIs.
- Data stored in DAX have a **TTL** of **5 minutes** (**default**).
-  Can deliver up to 10 times performance improvement—**from milliseconds to *microseconds***—even at millions of requests per second.

> [!question]- When to go for ElastiCache over DAX?
>- ElastiCache is useful in a scenario where the application is performing some computation after retrieving it from DynamoDB. The aggregation result is stored in ElastiCache. *If there is no compute then it is always advisable to use DAX*.
>- Also using Elasticache with DynamoDB is much more involved than DAX.

## DynamoDB Streams
- *Event driven programming* using **dynamo db streams**. 
	- Example sending a welcome mail when users are added: Enable DynamoDB Stream and create an AWS Lambda trigger, as well as the IAM role which contains all of the permissions that the Lambda function will need at runtime. The data from the stream record will be processed by the Lambda function which will then publish a message to SNS Topic that will notify the subscribers via email.

- Ordered stream of **item-level modifications** (create/update/delete) in a table
- DynamoDB streams is **not enabled by default**.
- Stream records can be sent to (**3**) : **Lambda**, **Kinesis Data Streams** and **Kinesis Client Library applications**.
- *Data retention* for up to **24 hours**.

## DynamoDB Global Tables
- Tables are present in **different regions**.
- There is **two way replication** between the tables.
- This will make DynamoDB tables accessible with **low latency** in **multiple regions**.
- It is an **Active Active** replication which means **data can be READ and WRITTEN to the table in any region**.
- **DynamoDB streams must be enabled** to use this feature.

> [!note]+ Here **active active** configuration is the key. 
> - You will be presented with questions in which you will have to choose between DynamoDB global tables and [[Aurora#Global Aurora|Global Aurora]] for a database that spans *multiple regions*.
> - If the question mentions *active active* then go for DynamoDB tables since in Global Aurora you cannot have active active config. There is *only one master and read replicas* in other regions for low latency. The read replicas don't take writes.
> - We do have [[Aurora#Aurora Multi Master|Aurora Multi Master]] in which all the databases take writes but it is not multi region.
> - So we can say **DynamoDB global tables** are **multi master**, **multi region** 
> - Whereas **Aurora Global** is **single master**, **multi region**.

## DynamoDB TTL
- It is possible to *delete items in DynamoDB after a certain time automatically*.
- Use case: *deleting expired cookies of users* and then prompting them to login again.

## DynamoDB Indexes
- There are **two** types of indexes **Global Secondary Indexes (GSI)** & **Local Secondary Indexes (LSI)**.
- These indexes allow us to query items on attributes other than the primary key.
- The optimal usage of a table's provisioned throughput depends not only on the workload patterns of individual items, but also on the *partition-key design*.
	- More the *distinct partition key values* that your workload accesses, the more those requests will be spread across the partitioned space. 
	- Use of *partition keys with high-cardinality attributes*, which have a **large number of distinct values** for each item.
