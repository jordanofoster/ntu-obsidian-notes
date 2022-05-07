### Scheduling Policies and Algorithms
Two policies:
- **Non-preemptive**
	- Processes run till complete or **BLOCKED**
- **Preemptive**
	- Processes can be interrupted/replaced
		- Generally via **timer interrupts**

There are also **six major scheduling algorithms** under the above two policies:

#### Non-preemptive Algorithms:

##### First Come, First Serve/First In, First Out (**FCFS/FIFO**)

- The processor is assigned to the **first process in the list**
	- This tends to favor queues with many **long jobs**
- In the interest of fairness, the ratio between wait and runtime should be roughly **the same for each process.**
	
#### Shortest Job First (**SJF**)
- Selects the job with the **shortest estimated run time**
	- Naturally, **short jobs** perform better
- Similar ratio to FIFO but **long jobs are starved by shorter processes** 
		
#### Preemptive Algorithms:

##### Shortest Remaining Time (**SRT**)
- **Preemptive equivalent of SJF** - chooses based on shortest estimated **remaining** time
	- If a new job with a **shorter runtime** than the current process appears, it will be **started immediately**
- As with SJF, short jobs favoured, long jobs starved
- **Increased system overhead** compared to SJF due to need to **measure elapsed runtime** 
		
##### Highest Response Ratio Next (**HRRN**)
- **Derived from SJF** to reduce **long job bias by reducing starvation**
- Jobs are **assigned priorities**
	- This is based on the following:
		- **Memory**
		- **Time**
		- Other resource requirements **\[(waiting time + run time) / run time\]**
- Job with **highest priority goes first**
- Priorities can change when **new jobs are added**

##### Round Robin (**RR**)
	
- CPU assigned to processes in turn using fixed **time quantum** (~10-20ms, lower with higher-clock processors)
- Processes running over designated time **interrupted, moved to back of queue**
- **Heavy overhead** due to constant switching.
	
##### Multi-level Feedback Queues (**MFQ**)

- Technically, **not another scheduling algorithm**
- Consists of **several independent queues**
	- Using **other existing algorithms**
- **Each queue has different priority**
- Useful to maintain common processes (e.g. I/O jobs in one queue, CPU jobs in another)
- Jobs able to **move to other queues** 
	- dependant on **priority change**

### Scheduling in Distributed Systems
	NOTE: To be discussed next term in Topic 9

In distributed computing scheduling becomes more of a **routing problem** and ensuring that **no one node is over/under loaded.**

Number of methods, some shared with OSes:
- Round robin
- Priority based (**weighted round robin**)
- Sender / reciever initiated
- Least connection/Least loaded
- Min-min
- Max-min
- Opportunistic load balancing
- Equally spread current execution
- Throttled load balancing
- Ant colony optimisation
