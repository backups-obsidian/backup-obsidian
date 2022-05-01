---
created: 2022-04-19 16:22
updated: 2022-05-01 21:38
---
---
**Links**: [[101 AWS SAA Index]]

---

## RDS Read Replica
- Read replicas help in scaling our reads.
- With RDS non [[Aurora]] engines we can create upto **5** read replicas.

> [!important] Read replicas can be in the *same AZ*, *different AZ* or in a *different region*.

- Replication is **async** so the reads are **eventually consistent**.

> [!caution]- Read replicas can be **manually** promoted to their own DB i.e. allowing it to take writes. But by **default they only read**.
> That is by default read replicas are only used for **SELECT** statements.

- To take advantage of the read replicas the *application must update the connection string*. You don't have to update the connection string in Aurora.

> [!tip]- Classic use case of Read Replicas
> **Reporting application** wants to read you data. You create a read replica for it. Reading from the main database will effect the performance of production application.

- In AWS there is a *cost when data goes from one AZ to another*. For *RDS read replicas* if its in the *same region then we don’t have to pay this fee*.
	- ![[attachments/Pasted image 20220421121900.png]]
	- Read Replicas are *billed as a standard DB Instance and at the same rates*. You are not charged for the data transfer incurred in replicating data between your source DB instance and read replica within the same AWS Region.

> [!question]+ How to create a *high availability read replica*?
> You can create a **read replica as a Multi-AZ DB instance**. Amazon RDS creates a standby of your replica in another Availability Zone for failover support for the replica. *Creating your read replica as a Multi-AZ DB instance is **independent** of whether the source database is a Multi-AZ DB instance*.

## RDS Multi AZ
- Spans at least 2 AZ. As the name suggests the standby instance is in a different AZ in the same region.
- Replication is **sync**.
- We have a **single DNS name** which **switches automatically**(**Automatic failover**) to the standby database in case the primary database becomes unavailable. 
	- We can say the *CAME record* will be updated to point to the standby DB.
- Automatic failover takes places in case (**3**) of: 
	- Loss of AZ
	- Storage failure on primary 
	- Loss of network

> [!important]- The standby database in Multi AZ is *not used for scaling*. **No one can read to it or write to it**. It is just here as a failover.
> Remember *high-availability feature is not a scaling solution for read-only scenarios*; you cannot use a standby replica to serve read traffic. To service read-only traffic, you should use a Read Replica.

- With Multi AZ we get increased database availability in case of system upgrades like OS patching or DB instance scaling.

> [!question]- Why not use Read Replica for disaster recovery?
> Read replicas can be setup in a different AZ for disaster recovery. Although you can promote a read replica, its *asynchronous replication might not provide you the latest version of your database*. **Always go for multi AZ for disaster recovery**.

> [!tip]- If you see key words like *high availability* and *automatic failover* then always go for RDS multi AZ. 
> Although you can have read replicas in different regions they don't offer automatic failover. You have to manually promote it.

- We can easily configure a RDS database to be multi AZ by enabling it in settings.
- What happens when you *convert a single AZ database to multi AZ*?
	- AWS automatically takes a *snapshot of our DB*, 
	- Creates a *new DB from the snapshot* 
	- Establishes *sync replication*