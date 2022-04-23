---
created: 2022-04-19 16:22
updated: 2022-04-20 20:35
---
---
**Links**: [[101 AWS SAA Index]]

---
-   **Launch configuration** is **legacy**
-   **Launch template** is the **newer** version

- In **launch templates** we can have:
	- Multiple versions
	- We can use inheritance by creating partial launch templates
	- We can **provision a mix of on demand and spot instances**. This is not possible in launch configuration.
	
>[!info] To remember T > C.

- Launch templates are recommended by AWS.
- Launch configurations cannot be versioned and you have to create new ones every time if you want to make any changes. They cannot be modified.