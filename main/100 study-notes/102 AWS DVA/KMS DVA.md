---
created: 2022-05-30 12:29
updated: 2022-06-01 12:08
---
---
**Links**: [[102 AWS DVA Index]]

---
## KMS Limits
- When you exceed a request quota, you get a **ThrottlingException**
- For cryptographic operations (like encrypt, decrypt, GenerateDateKey etc) , they *share a quota*. 
	- This includes *requests made by AWS services on your behalf* (ex: SSE-KMS)
- How to deal with KMS limits:
	- Use *exponential backoff* (backoff and retry)
	- *For GenerateDataKey*, consider using *DEK caching* from the Encryption SDK
	- You can request a *Request Quotas increase through API or AWS support* 

## S3 & KMS
### Forcing S3 SSL and KMS
- To force SSL, create an S3 bucket policy with a **DENY on the condition** `aws:Secure Transport = false`
- Forcing encryption:
	- *Deny incorrect encryption header*: make sure it includes `aws:kms` (== SSE-KMS)
	- *Deny no encryption header* to ensure objects are not uploaded un-encrypted

### S3 Bucket Key
- New setting to **decrease** 
	- Number of API calls made to KMS from S3 by *99%*
	- Costs of overall KMS encryption with Amazon S3 by 99%
- This leverages *data keys*
	- A S3 bucket key is generated
	- That key is used to encrypt KMS objects with new data keys
	- ![[attachments/Pasted image 20220601120714.png]]
- You will see *less KMS CloudTrail events* in CloudTrail

