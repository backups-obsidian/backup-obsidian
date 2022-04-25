---
created: 2022-04-19 16:22
updated: 2022-04-25 20:45
---
---
**Links**: [[101 AWS SAA Index]]

---
## ECR
-  It stands for **Elastic Container Registry**.
- It is used to **store, manage and deploy AWS containers**.
- You pay for what you use.
- EC2 instances will *pull the images from ECR* to create containers. It can do so because of *instance role* (EC2 instance profile) permissions.

## EKS
- Stands for **Elastic Kubernetes Service**
- Launch **managed** **Kubernetes cluster** on AWS
- It has a similar goal as ECS but is **open source**. Kubernetes is *cloud agnostic*.
- It supports **2 launch modes**: **EC2** and **Fargate**
- It provides a **fully-managed control plane** so you would not have access to the EC2 instances that the platform runs on.
- EKS pods run on EKS nodes. Here **EKS pods are similar to ECS tasks**.