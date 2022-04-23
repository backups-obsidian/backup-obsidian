---

---

## Regions

-   AWS has `regions` all around the world.
egions have a codes like `us-east-1`, `eu-west-3`. Each region has a code mapped to a name. We can also see this in the console.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9219afc-63ec-4dcc-9b2d-a07937c94f6a/Untitled.png)
    
-   **A region is a cluster of data centers**
    

<aside> ℹ️ Most AWS services are region scoped

</aside>

This means if you use a service in one region and then use it in another region then it will be like you are [using](obsidian://open?vault=test&file=main%20note) the service for the first time.

-   **Important Services which are Global** → `IAM, Route 53, CloudFront`
    
    Once you select a Global service you will see service does not require region selection.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8384306-5082-4be5-a1c4-32d4fe2aa905/Untitled.png)
    
    If you select a region scoped service like EC2 you can choose a region.
    

Important Service which are **region scoped** → `EC2, Lambda`

<aside> ℹ️ All services may not be present in one region so switch to another region if you want to use that service.

</aside>

### How to choose an AWS region → It depends on a lot of factors (GDPR, latency, services, price)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/767af82c-ab5c-4175-8011-b50a3205440a/Untitled.png)

If you are trying on something then choose a region closest to you.

## Availability Zones

-   **In each region we have multiple** `Availability Zones` **(AZs)**
-   Each region has many AZs. **Usually 3, min (2), max (6)**
-   **Each (AZ) has one or more discrete data centers** with redundant power, networking, and connectivity.
-   **The AZs are separated from each other so that they are isolated from disasters.** So that there is no cascading effect if one of the AZs goes down.
-   All the AZs are connected via high bandwidth low latency networking. Once connected it forms a region.

### Example of AZs

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8db604d9-3e34-48cb-a024-0a8858f15117/Untitled.png)

Notice that the region code is `ap-southeast-2` and the codes for AZs are ap-southeast-**2a,2b and 2c**.

## Edge Locations

-   They are also known as **Points of Presence (PoP)**
   fdsfs 
-   Cloudfront
    
-   More info
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d0584f0-a7a3-432b-a100-cf26e9526068/Untitled.png)

# hello

