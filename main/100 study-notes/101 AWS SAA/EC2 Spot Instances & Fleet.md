---
created: 2022-04-19 19:08
updated: 2022-04-19 19:25
---
---
**Links**: [[101 AWS SAA Index]]

---
## Spot Request
- To get a spot instance we create a **Spot Request**.
- The spot request can be **one time** or **persistent**.
- A spot request has the following required parameters defined by us → `max price`, `no of instances`, `request type`, `valid from to valid until(can be infinite)`, `launch specification (ami)`

### The difference between one time and persistent request
-   **One Time request** → once the request is *fulfilled* instances are launched and the *spot request will go away*.
-   **Persistent** → we want x number of instances from the spot request *as long as the spot request is valid* (`valid from → valid until`). If the instances are stopped because current spot price > max price then the spot request will go back into action and will restart the instances when spot price < max price.

> [!info] Cancelling a spot request does not terminate the instances. So it is our responsibility to terminate the running instances.

> [!question]- How to terminate instances in a persistent request?
> To terminate all the spot instances in a persistent request you must *first cancel the the spot request* and *then terminate the instances*. Since in a persistent request *if you terminate the spot instances first* then the *feedback loop* will see that x number of instances were needed but there are 0 now so it *will start them again*.

## Spot Fleets
- Set of **spot instances** + optional **on demand instances**.
- We define **launch pools**.
- Spot fleet *stops* when *maximum capacity* is reached *or* *maximum cost* defined by us is reached.
- Spot fleet allows us to **automatically request instances with the lowest price**.
- By default, Spot Fleets are set to maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated.
- Strategies to launch spot instances: **lowestPrice** (*short workloads*), **diversified**(*long workloads*), **capacityOptimised**.