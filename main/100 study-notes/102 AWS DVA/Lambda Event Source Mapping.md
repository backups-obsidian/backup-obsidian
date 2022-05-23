---
created: 2022-05-23 17:00
updated: 2022-05-23 17:03
---
---
**Links**: [[102 AWS DVA Index]]

---
- Services:
	- *Kinesis Data Streams*
	- *SQS & SQS FIFO queue*
	- *DynamoDB Streams*
- Records need to be **polled** from the source. This means lambda needs to ask the services for some records.
- Lambda is invoked **synchronously**.
-  This is test to see if its working