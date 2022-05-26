---
created: 2022-05-26 10:19
updated: 2022-05-26 10:42
---
---
**Links**: [[300 home]]

---
- *Most developers always associate REST with HTTP and that’s where the confusion arises*.
- HTTP API is also known as a web API

> [!note]+ **Any transfer protocol can be used to create a RESTful API**. 
> - REST is not necessarily tied to HTTP. 
> - Rest is an *architectural style* which may use HTTP, FTP or other communication protocols but is widely used with HTTP.

- *RESTful web services* are just web services that *follow a RESTful architecture*
- **HTTP is a contract, a communication protocol and REST is a concept**. 
	- REST implies a *series of constraints (6)* about how Server and Client should interact. 
	- HTTP is a communication protocol with a given mechanism for server-client data transfer. 

- An *HTTP API simply only says that the HTTP protocol is used*. A HTTP API doesn't necessarily have to be a REST API if it doesn't follow REST architectural styles.
	- This means that *even SOAP* (Simple Object Access Protocol) can be *regarded as HTTP API* if it uses HTTP for transport

> [!caution]- If the constraints specified by the REST is not met then the API is just an HTTP API and not a REST API.