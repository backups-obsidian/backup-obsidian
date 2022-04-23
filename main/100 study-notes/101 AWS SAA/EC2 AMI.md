---
created: 2022-04-19 16:22
updated: 2022-04-20 10:44
---
---
**Links**: [[101 AWS SAA Index]]

---
- Built for a **specific region**. **Can be copied to other regions**.
- If you have a *custom AMI then the boot time will be faster*. You have to make and maintain you own custom AMIs.
- There are 3 options for AMIs: 
	- *Public*: AWS provided 
	- *Marketplace*: Made by someone else and potentially sold.
	- *Custom AMIs*: Made and maintained by us.
- **AMIs are stored in S3** but we cannot view them.
- We can copy EBS and instance store backed AMIs. 
- There are *no charges on copying an AMI*. 

> [!important] When the new AMI is copied from region A into region B, it **automatically creates a snapshot in region B because AMIs are based on the underlying snapshots**. 

> [!info]- If you copy an EBS-backed AMI, you will incur charges for the storage of any additional EBS snapshots.
> This means when you copy an EBS backed AMI from an EC2 instance a snapshot is made of the EBS volume. So when AMIs are copied to other regions EBS snapshots are also copied. When you create an EC2 instance from the copied AMI the copied EBS snapshot is used to create a volume.

> [!tip]+ AMIs can help in disaster recovery. How?
> - You can copy an Amazon Machine Image (AMI) of an EC2 instance (EBS volume is also copied) and specify the second Region for the destination.
> - Launch a new EC2 instance from an Amazon Machine Image (AMI) in the second Region

