---
created: 2022-05-29 16:01
updated: 2022-06-06 19:20
---
---
**Links**: [[103 Golang Index]]

---
## Concurrency vs Parallelism
- Concurrency means loading more goroutines at a time. If one goroutine blocks, another one is picked up and started. *On single core CPU you can run ONLY concurrent applications but they are not run in parallel*.
- **Parallelism means multiple goroutines executed at the same time**. 
	- It requires *multiple CPUs*.
- *Concurrency means independently executing processes* or dealing with multiple things at once, **while parallelism is the simultaneous execution of processes** and require multiple core CPUs.
- **Concurrency means context switching**.
	- CPU time is divided between different processes.

## Goroutines
- A goroutine is a **lightweight thread of execution** 
	- Goroutines are key ingredients to achieve concurrency in Go.
- A **goroutine is a function** that is capable of running concurrently with other functions. 
- To create a goroutine we use the *keyword* `go` *followed by a function invocation*
- Goroutines are *far smaller that threads*, they *typically take around 2kB* of stack space to initialise compared to a *thread* which takes a fixed size of *1-2Mb*.
- An *OS Thread Stack is fixed size* but a **goroutine stack size shrinks and grows as needed**.
- *OS threads are scheduled by the OS kernel*, but *goroutines are scheduled by its own Go Scheduler* using a technique called **`m:n` scheduling**, because it multiplexes (or schedules) *m goroutines on n OS threads*.
	- Scheduling a goroutine is much cheaper than scheduling a thread.
- Goroutines have **no identity**. There is no notion of identity that is accessible to the programmer.
