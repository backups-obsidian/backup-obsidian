---
created: 2022-04-22 22:17
updated: 2022-04-25 23:08
---
---
**Links**: [[300 home]]

---
## Why gRPC
- Today's trend is to build micro services. For these services to communicate with each other we need APIs. 
- Standard approach is to build REST APIs. But it comes with a lot of problems. Like:
	- You need to think about the endpoint.
	- You need to think about how to invoke the API and how to handle errors.
	- You need to think about efficiency, latency, interoperability etc,
	- You need to think about logging, authentication etc.

- gRPC aims to solve all the above problems.

## What is gRPC
- It is a *free and open source* framework developed by *google*. It is now a part of CNCF (Cloud Native Computing Foundation) like Kubernetes and Prometheus.
- At a high level, it allows you to define REQUEST and RESPONSE for *RPC (Remote Procedure Calls)* and handles all the rest for you.
- On top of it, it's *modern*, *fast and efficient*, build on top of **HTTP/2**, *low latency*, supports *streaming*, *language independent*, and makes it super easy to plug in *authentication*, load balancing, *logging and monitoring*.
- It is best for building *micro services*.

> [!question]- What is RPC?
> - An RPC is a Remote Procedure Call.
> - In your CLIENT code, it *looks like you're just calling a function directly on the SERVER*.
> ---
> ![[attachments/Pasted image 20220422222840.png]]

- RPC is not a new concept but in gRPC it has been implemented cleanly and solves a lot of problems
- At the core of gRPC, you need to *define the messages and services* using **Protocol Buffers**
- The rest of the gRPC code will be generated for you and you'll have to provide an implementation for it.
- One `.proto` file works for over 12 programming languages (server and client), and allows you to use a framework that scales to millions of RPC per seconds.
	- ![[attachments/Pasted image 20220425223839.png]]

- In gRPC data is *serialised*. Serialising takes complex data and lists it in a sequential manner. This is what pickle (python library for writing to files) does under the hood.
	- Some serialisation formats are JSON and protobuf. 
	- JSON is serialised in plain text, protobuf in *binary*.
	- JSON is great when you have small volume of message exchange where as protobuf is great when you have a high volume of message exchange.
	- *Protobuf* is something *you would use if performance really matters*.





