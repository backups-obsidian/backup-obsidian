---
created: 2022-05-16 16:54
updated: 2022-05-26 20:17
---
---
**Links**: [[102 AWS DVA Index]]

---
- The mean reason for using API Gateway over ALB for invoking Lambda's from HTTP endpoints are the features (like caching and all) offered by the API Gateway.

## Deployment Stages
- Making changes in the API Gateway does not mean they're effective. You need to make a *deployment for them to be in effect*.
- **Changes are deployed to Stages** (as many as you want)
	- Use the naming you like for stages (dev, test, prod)
	- Each *stage has its own configuration parameters*
	- *Stages can be rolled back* as a history of deployments is kept
- We can have *multiple stages* deployed together. 
	- A common use case is to have 2 stages v1 and v2 to *maintain compatibility*. 
	- We can migrate the clients from v1 to v2 gradually and when no more clients are using v1 we can shut it down.
	- ![[attachments/Pasted image 20220526151955.png]]
- Each stage has its own settings
	- ![[attachments/Pasted image 20220526153838.png]]

### Stage Variables
- Stage variables are like **environment variables for API Gateway**
- Use them to change *often changing configuration values*
- They can be used in:
	- *Lambda function ARN*
	- *HTTP Endpoint*
	- Parameter mapping templates
- Use cases:
	- Configure HTTP endpoints your stages talk to (dev, test, prod...)
	- Pass configuration parameters to AWS Lambda through mapping templates
- Stage variables are passed to the **context object in AWS Lambda**

#### Stage Variables & Aliases
- We create a *stage variable to indicate the corresponding Lambda alias*
- Our API gateway will automatically invoke the right Lambda function!
	- ![[attachments/Pasted image 20220526152359.png]]
	- ![[attachments/Pasted image 20220526152601.png]]
	- ![[attachments/Pasted image 20220526153218.png]]

## Canary Deployments
- Possibility to enable canary deployments **for any stage (usually prod)**
	- ![[attachments/Pasted image 20220526154203.png]]
- Choose the *% of traffic* the canary channel receives 
	- ![[attachments/Pasted image 20220526154031.png]]
- Metrics & Logs are separate (for better monitoring)
- Possibility to override stage variables for canary
- This is **blue/green deployment** with AWS Lambda & API Gateway

## Swagger / Open API spec
- We can *import existing* Swagger / OpenAPI 3.0 spec to API Gateway
- We can also *export current API* as Swagger / OpenAPI spec
- *JSON or YAML file*
- Once imported API will be created from the JSON/YAML document.

## Usage Plans & API Keys
- If you want to *make an API available as an offering ($) to your customers*
- **Usage Plan**:
	- *Who can access* one or more deployed API stages and methods
	- *How much and how fast* they can access them
	- Uses *API keys to identify API clients and meter access*
	- *Configure throttling limits and quota* limits that are enforced on individual client
- **API Keys**:
	- Alphanumeric string values to distribute to your customers
	- Can use with *usage plans to control access*
	- **Throttling limits are applied to the API keys**
	- Quotas limits is the overall number of maximum requests
- **Configuring a usage plan**: 
	- Create one or more APIs, *configure the methods to require an API key*, and deploy the APIs to stages.
	- *Generate or import API keys* to distribute to application developers (your customers) who will be using your API.
	- *Create the usage plan* with the desired throttle and quota limits.
	- *Associate API stages and API keys with the usage plan*.

> [!tip] Usage plan order: Create API -> Create Key -> Create Usage Plan -> Associate Usage Plan

> [!note] Callers of the API must supply an assigned API key In the `x-api-key` header in requests to the API

## HTTP API vs REST API
- HTTP APIs
	- **low-latency**, **cost-effective** AWS Lambda proxy, HTTP proxy APIs and private integration (no data mapping). **Only proxies**.
	- Support *OIDC* and *OAuth 2.0*
	- Authorisation, and built-in support for CORS 
	- No usage plans and API keys
- REST APIs
	- All features (**except Native OpenID Connect / OAuth 2.0**)

> [!note]- For exam perspective just remember 
> - HTTP API is a *low cost alternative* 
> - It *only supports proxy integrations* 
> - There is no such thing as usage plan and API keys.

