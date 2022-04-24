---
created: 2022-04-18 19:08
updated: 2022-04-19 10:01
---
---
**Links**: [[101 AWS SAA Index]]

---
## Terminologies
-   IAM **Resources** → `user`, `group`, `role`, `policy`, and identity provider objects that are stored in IAM.
-   IAM **Identities** → The IAM resource objects that are used to identify and group. *You can attach a policy to an IAM identity*. These include `users`, `groups`, and `roles`.
-   IAM **Entities** → The IAM resource objects that AWS **uses for authentication**. These include IAM `users` and `roles`.
-   IAM **Principals** → A person or application that uses the `AWS account root user`, an `IAM user`, or an `IAM role` to **sign in and make requests to AWS**. Principals include federated users and assumed roles.

## Introduction
- **Global** service. Existing IAM roles can be *assigned to services in any region*.
- When we first create an AWS account we actually create an IAM root account
- IAM is **eventually consistent**. It takes time to become visible from all possible endpoints.

> [!TIP]- Don't use root user
> Root user can do anything it wants. We should create administrator account to manage everything.
## Users and Groups
- *Newly created users don't have any permissions*.
- IAM users are not separate accounts, they are users within the same account.
- You give permissions to **IAM Identities** (Users, groups, roles) by attaching policies. 
- **Groups can only contain users and not other groups**.
- Users don't have to belong to a group but it is a best practice to keep them in groups. 
- *A single user can belong to multiple groups*.

 > [!attention]+ What groups can't do.
 > Groups are not IAM Principals so they *cannot assume roles*. Only **users** and **services** can assume roles.
- Groups are also **not** supported by **permission boundaries**.

## Policies
- Policies are nothing but **JSON** documents.
- A policy can consist of multiple statement and each statement can have **6** fields. These fields in policy are **Principal**, **Effect**, **Action**, **Resource**, **SID** (optional), **conditions** (optional).
	- *Principal*: The user/account/role to which this policy is applied.
	- *Effect*: Allow/Deny
	- *Action*: Things you are allowed to perform like get on a s3 bucket.
	- *Resource*: The buckets on which you can perform the action.
- Always follow the principle of **least privileged** when assigning policies.

 - **Sample Policy**
	 - ![[attachments/Pasted image 20220418193200.png]]
- We can also simulate the IAM policies using the **policy simulator** provided by AWS
- **Conditions** help in making the IAM policy **more restrictive**. 
	- We can have an explicit deny if the sourceIP is not = required value. 
	- We can restrict regions *to which* API calls can be made using `aws:RequestedRegion`.
	- We can restrict based on tags.
	- We can force MFA

### Tag based policies
- We can *use tags for assigning policies* like who has access to production and staging servers. 

> [!tip]+ How does it work?
> Add a specific tag to the instances you want to grant the users or groups access to. *Create an IAM policy that grants access to any instances with the specific tag*.

## Account Security
- There are two ways of securing the account. 
	- Password Policy: Strong password
	- MFA

## Different ways of accessing IAM accounts

- We can use IAM console (web), CLI, SDK.
- For using **CLI** and **SDK** we need to generate **Access Keys**. 
- Access Keys are generated from the management console for each user.
- Access keys are just like username and password so **never share it**. 
- `Access key id` ~ username, `Secret Access Key` ~ password.

> [!attention]- Access Keys != Permissions
> Generating access keys for a user doesn't mean that you will be able to make API calls using the CLI or SDK you need to have the right policies attached to you.

 - CLI is built on top of AWS python SDK.
 - All the CLI commands start with `aws`.
 
> [!tip]- Don't loose you access keys
> If you lose or forget your secret key, you cannot retrieve it. Instead, create a new access key and make the old key inactive. You only see the access key at the time of creation

- We can also access the AWS CLI using the **cloud shell**. It is not accessible in all regions.
- Use `aws configure` to configure the CLI by providing the region, key and secret id.

>[!attention]+ Default region
> If you don't provide the region in CLI or SDK then it will default to `us-east-1`

## IAM Roles
- We assign permissions to AWS services using Roles.

>[!attention]+ What is the purpose of a role
> A role is intended to be assumable by anyone who needs it. Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.

- The **temporary credentials** are generated by **STS**.
- An IAM role can be assumed by the following: ^fe4632
	- *AWS Services*: Like giving permission to EC2 to upload to S3.
	- *AWS Accounts*: For **cross account access**.
	- *Web Identity*: Allows users **federated** by the specified external *web identity* provider to *assume this role* to perform actions in this account.
	- *SAML 2.0 federation*: Allow users federated with SAML 2.0 from a **corporate directory** to perform actions in this account. 
	- *Custom trust policy*: 

- An IAM user in the same account can also assume a role. [[STS & Identity Federation#^a42567|But why do it]].
- **Service-linked roles** are predefined by the service and include all the permissions that the service requires to **call other AWS services on your behalf**.
- We cannot create service based roles, they are created by AWS with predefined policies.

>[!question]- A developer needs to implement a Lambda function in AWS account A that accesses an Amazon S3 bucket in AWS account B.
> Create an IAM role for the Lambda function that grants access to the S3 bucket. Set the IAM role as the Lambda function's execution role. **Make sure that the bucket policy also grants access to the Lambda function's execution role**.
> ---
> **If** the IAM role that you create for the Lambda function is in the same **AWS account as the bucket, then you don't need to grant Amazon S3 permissions on both the IAM role and the bucket policy**. Instead, you can grant the permissions on the IAM role and then verify that the bucket policy doesn't explicitly deny access to the Lambda function role. If the IAM role and the bucket are in different accounts, then you need to grant Amazon S3 permissions on both the lAM role and the bucket policy.

## Resource based policies
- Resource based policies are supported by **S3**, **SNS**, **SQS**
- They help in facilitating **cross account access** of these resources.
- **Resource based policies** for S3 are also known as **bucket policies**.

> [!question]+ Why use Resource based policies when you can assume a role for cross account access?
> We can easily create a role in the account where S3 is present and assume that role using STS. Here *role acts as proxy*.
> ---
> They look similar but there is a difference. *When you assume a role (user, application or service), you give up your original permissions and take the permissions assigned to the role*. When using a resource based policy the *principal doesn’t have to give up his permissions*.

- Example use case: User in account A needs to scan a DynamoDB table in Account A and dump it in an S3 bucket in Account B. If we use an IAM role to do something in Account B then we won’t be able to do anything in Account A.

## Security Tools
- **IAM Credentials Report**:
	- *Account Level*
	- A report that lists all your account's users and the *status of their various credentials*.

- **IAM Access Advisor**
	- *User Level*
	- Access advisor shows the service permissions granted to a user and when those services were last accessed.
	- You can use this information to *revise your policies*.

## Best Practices
- Don't use the root account except for AWS account setup
- One **physical user = One AWS user**
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication (MFA)
- Audit permissions of your account with the lAM Credentials Report
- Never share IAM users & Access Keys