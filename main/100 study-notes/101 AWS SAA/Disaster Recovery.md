---
created: 2022-04-19 16:22
updated: 2022-04-30 15:35
---
---
**Links**: [[101 AWS SAA Index]]

---
## RPO and RTO
- RPO → **Recovery Point Objective**
    - It is basically how often you run backups, *how back in time can you recover*.
    - RPO is **how much of data loss** are you willing to accept in case of a disaster.
- RTO → **Recovery Time Objective**
    -  Defines the **down time** after disaster.
- RPO and RTO visualised
	- ![[attachments/Pasted image 20220430153011.png]]

> [!note] Our target is to *decrease the RTO and RPO*
- *Cost increases* as the try to decrease RTO and RPO.

## DR Strategies
- List of strategies with RPO and RTO in decreasing order.
- **Backup & Restore** 
    - It is quite *cheap*. We *recreate infrastructure only when we have a disaster*.
    - Very *easy*.
- **Pilot Light**
    - A *small version of the app* is always running in the cloud.
    - Useful for the **critical core (pilot light)**
    - **Faster than Backup and Restore as critical systems are already up**
    - For example in the RDS will be running but not the EC2 instances so if some disaster strikes the on premise data centre then Route53 will manage the failover.
- **Warm Standby**
    - **Full system is up and running, but at minimum size**
    - Upon disaster, we can *scale to production load*
-   **Multi Site/ Hot Site approach**
	- **Full Production Scale** is running AWS and On Premise
