---
created: 2022-04-19 16:22
updated: 2022-04-19 19:40
---
---
**Links**: [[101 AWS SAA Index]]

---
- In EC2 Hibernate RAM is preserved in the EBS volume.
- Some **use cases** of this would be *saving the ram state* (redis) or *services that take a long time to initialise*.
- RAM size cannot be greater than **150 GB**.
- An instance cannot be hibernated for more than **60 days**.
- Hibernate is not supported on bare metal.

> [!caution] **Root** EBS volume must be **encrypted** to use hibernate.

> [!caution] **Instance storage** is not supported.
