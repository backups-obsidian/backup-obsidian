---
created: 2022-04-19 16:22
updated: 2022-04-30 11:37
---
---
**Links**: [[101 AWS SAA Index]]

---
- Capture information about **IP traffic** in the VPC.
- Used for [[GuardDuty]] for security.
- They can be at the **VPC level** or the **subnet level** or at the **interface level**. Go for interface level for more security
- They are very helpful in *troubleshooting connectivity issues*.
- The logs can be sent to **two destinations**: **S3** and **CloudWatch Logs**.
- They also **capture information for AWS managed interfaces** like ALB, ElastiCache, Redshift, NATGW etc
- The logs have a specific syntax and it is best to *analyse it using Athena*.