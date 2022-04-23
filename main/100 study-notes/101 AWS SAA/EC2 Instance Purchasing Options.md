---
created: 2022-04-19 11:14
updated: 2022-04-20 10:51
---
---
**Links**: [[101 AWS SAA Index]]

---
## On Demand Instances
- **Short uninterrupted** workload.
- More expensive than spot and reserved.

### Capacity Reservations
- We can do a **capacity reservation** of *on demand instances*. There is **no monetary benefit** but there is a guarantee that you will have capacity when you need it. This is particularly useful when you know that you will be needing an instances for an uninterrupted workload at a particular time.
- For monetary benefit you can use **capacity reservation with savings plan**.
- If you want to *make reservations in multiple AZs* then you need to file *multiple reservation requests*.
- The main benefit of capacity reservation over reserved instances is there is no need of 1 or 3 years of commitment.

## Reserved Instances
- Reserved Instances are *not physical instances*, but *rather a billing discount applied to the use of On Demand* Instances in your account.

### Standard Reserved
- **75%** cheaper than on demand.
- For stable applications like database.
- Commitment of **1 (minimum) or 3 years**. For 3 years you get more discounts.
- **Payment options** are *no upfront* (no discount), *partial upfront* (discount +) and *full upfront* (discount +++)
- We reserve a **specific instance type**.
- *Unused* Standard Reserved Instances *can later be sold* at the *Reserved Instance Marketplace*.

### Convertible Reserved 
- We can *change the instance type*.
- Less cost savings as compared to normal reserved.

>[!caution] Convertible unused instances **cannot be sold** in the Reserved instance marketplace.

## Spot
- Highest discount **90%** as compared to on demand.
- Can lose them at any moment.
- Suitable for batch jobs, data analysis etc.
- We get a spot instance if `current spot price < max spot price defined by us`. 
- If current spot price is greater then instance has to be stopped or terminated. We have a *grace period of 2 minutes*.
- Spot pricing can vary depending on AZ.

## Dedicated Hosts
- For **compliance** reasons and **server bound software licenses** (complex licensing, BYOL - Bring your own license).
- **3 year reservation**.
- Billing per host.
- With dedicated hosts you have additional control and visibility on how instances are placed on the server.
- With Dedicated Host the physical server is basically yours. It does not change, **it's always the same physical machine for as long as you are paying.**

## Dedicated Instances
- Instances running on hardware dedicated to you.
- Dedicated instances may share hardware with other instances from the same AWS account that are not dedicated instances. Dedicated instances *cannot be used for existing server-bound software licenses*.
- Billing per instance.
- *Automatic instance placement*.
- Your instance runs on some dedicated hardware. **Its not lockdown to you**. If you stop/start instance, you can get some other hardware somewhere else. Basically, the hardware is "yours" (*you are not sharing it with others) for the time your instance is running*. You stop/start it, you may get different physical machine later on (maybe older, maybe newer, maybe its specs will be a bit different), and so on. **So your instance is moved around on different physical servers - whichever is not occupied by others at the time.**
- If you see keyword **single tenancy** in questions then go for dedicated instances. Dedicated hosts also offers single tenancy but it is more expensive. So unless there is a demand for licensing go for dedicated instances.
