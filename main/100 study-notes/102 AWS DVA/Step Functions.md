---
created: 2022-05-30 12:29
updated: 2022-05-30 15:07
---
---
**Links**: [[102 AWS DVA Index]]

---
## Step Functions
- It allows us to **model our workflow as state machines**.
- Use cases:
	- Order fulfilment, Data processing
	- Web applications, Any workflow 
- Written in **JSON**
- Visualisation of the workflow and the execution of the workflow, as well as **history** (useful for debugging)
- Start workflow with *SDK call*, *API Gateway*, *Event Bridge* (CloudWatch Event)

### Task State
- **Do some work** in your state machine
- *Invoke one AWS service*
	- Can invoke a *Lambda function*
		- ![[attachments/Pasted image 20220530123640.png]]
	- Run an AWS Batch job
	- Run an *ECS task* and wait for it to complete
	- *Insert an item from DynamoDB*
	- Publish message to *SNS, SQS*
	- Launch another Step Function workflow
	- ![[attachments/Pasted image 20220530123451.png]]
- *Run an one Activity*
	- *EC2, Amazon ECS, on-premises*
	- Activities poll the Step functions for work
	- Activities send results back to Step Functions
	- ![[attachments/Pasted image 20220530123526.png]]

#### States
- *Choice State*: *Test for a condition* to send to a branch (or default branch)
- *Fail or Succeed State*: Stop execution with failure or success
- Pass State: Simply pass its input to its output or inject some fixed data, without performing work.
- Wait State: Provide a delay for a certain amount of time or until a specified time/date.
- Map State: Dynamically iterate steps
- **Parallel State**: Begin *parallel branches of execution*.

> [!question]- You want to orchestrate multiple Lambda functions and *wait for the result of all of them before making a final decision*. What do you recommend?
> Step Functions *Parallel States* and then one final Task State

### Error Handling
- Whole power of step functions
- **All the errors should be handled in the state machine outside of the application code**.
- Any state can encounter *runtime errors* for various reasons:
	- State *machine definition issues* (for example, no matching rule in a Choice state)
	- *Task failures* (for example, an exception in a Lambda function)
	- Transient issues (for example, network partition events)
- Use **Retry** (to retry failed state) and **Catch** (transition to failure path) in the State Machine to handle the errors instead of inside the Application Code.
- Predefined error codes:
	- `States.ALL` : matches any error name
	- `States.Timeout`: Task *ran longer* than `TimeoutSeconds` or no heartbeat received
	- `States.TaskFailed`: *execution failure*
	- `States.Permissions`: insufficient privileges to execute code
- The state may report is own errors

#### Retry 
- **Evaluated from top to bottom**
	- ![[attachments/Pasted image 20220530125551.png]]
- *ErrorEquals*: match a specific kind of error
- *IntervalSeconds*: initial delay before retrying
- *BackoffRate*: multiple the delay after each retry
- *MaxAttempts*: default to 3, set to 0 for never retried
- When **max attempts are reached, the Catch kicks in**
- In the above example we see that changing the *error handling logic is very easy*.
	- If all these steps would have been inside the lambda function it might have timed out.

#### Catch
- **Evaluated from top to bottom**
	- ![[attachments/Pasted image 20220530125903.png]]
- *ErrorEquals*: match a specific kind of error
- *Next*: State to send to
- **ResultPath**: A path that determines what input is sent to the state specified in the Next field.
	- ResultPath is how you pass errors from the input to the output 
	- ![[attachments/Pasted image 20220530130227.png]]

### Standard vs Express Workflow
- *Express workflows* are *cheaper*, *run for shorter duration*(**5 minutes**) and *don't have an execution history*.
	- ![[attachments/Pasted image 20220530141934.png]]

