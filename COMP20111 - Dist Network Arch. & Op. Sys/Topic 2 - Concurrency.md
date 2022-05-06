#COMP2011-DNAOS/concurrency
# Concurrency
- Operating systems have different architecture layers; userland, kernelspace, and bare-metal (hardware).
- Hardware layer consists of microcode and software such as the BIOS, CPU, MMU and others.
- Kernels handle drivers, system security, configurations, I/O handling and process scheduling, among many other tasks. Kernels **act as an abstraction of hardware** for the purposes of compatibility.
- Higher-level segments of the kernel stack handle situations such as interrupts and CPU scheduling/synchronisation.
- The usermode layer consists of APIs and Syscalls for use by programmers and/or users.


## Programs and Processes

**Programs** are the compiled binary of written code; a **process** is a running instance of a program binary.

**Several processes** derived from the **same program** may be launched within a standard OS. each process is given its own **address space,** which is a **range of memory addresses** that can be read/written to by the process itself.

## Process Life Cycle

### Process Creation
Processes are created via one of **two methods:**
- The program is explicitly **executed** by the **user...**
- or by being executed by **another process** - this is called **spawning/forking.**
	- In the latter, the process that created another is known as a **parent** - and the process it spawned its **child.**
	- Child processes can also spawn their own processes, **making a tree.**
	
#### Process Table
	
New processes are given a unique Process Identification Number (**PID**) which is stored in a table by the OS.

Each process has its own data structure called a Process Control Block (**PCB**) which holds information about it called **Process Descriptors** as seen below:

![[Process Descriptors.png]]

### State Queues

Processes can only ever be in one of **three states:**
-	**RUNNING** on the CPU itself
	-	There can only ever be **at most one process in this state** at a time
-	**READY** but waiting for the CPU to be free
	-	in a queue of others in the same state
-	**BLOCKED** because of required resources being unavailable.
	-	processes are in a queue relating to the resource they are waiting to be open (I/O, storage, etc.)

![[StateQueue.png]]

### Process termination

Processes can terminate **voluntarily** or **involuntarily.**

Processes terminate voluntarily via two methods:
- **Normal exit** - the process finishes its work
- **Error exit** - the process has built in error handling and has caught such an error.

And involuntarily via two other methods:
- **Fatal error** - detected by OS itself (e.g. division by zero)
- **Killed** - by another process through the OS via a syscall.

## Process Execution

CPUs execute processes through the **Fetch-Execute** cycle, shown below:

![[FetchExecute.png]]

There are, however, **scenarios in which the CPU must break this cycle temporarily** - such as when a **blocked** process cannot be attended to or an extremely high-priority process needs immediate attention.

### Interrupts

Interrupts are signals sent to the CPU to indicate a hardware/software event that requires **immediate attention.** An example including an I/O event is listed below:
- I/O event occurs. process execution is **suspended** as no more progress can be made.
- Processor switches execution to **another process,** working on that instead.
- I/O event resolves and alerts CPU via an **interrupt.** CPU switches to handling the Interrupt Service Routine (**ISR**), a process specifically designed for **dealing with interrrupts.**
- The previously suspended process **continues where it left off,** if **conditions to do so are met.**

There are many types of interrupts, but here are three examples:
- An **I/O interrupt** is caused by an I/O device to signal completion or an error.
- A **Timer interrupt** is caused by a processor timer to alert the OS at given times.
- A **Program interupt** is caused by errors, both fatal and non-fatal (user processes).

Interrupts are the main mechanism by which OSes are able to perform **multitasking** - by overseeing several programs and I/O devices simultaneously.

With this additional knowledge, the Fetch-Execute cycle looks a bit more like this:

![[FetchExecuteInterrupt.png]]

## Concurrency
Single core processors can only execute **one instruction at a time.** the processor continues to work on a process until one of the following occurs:
- The process issues an I/O request via syscall
- An interrupt occurs

When a user process is suspended, the OS takes over by either **handling the I/O request** or starting the **interrupt handler.** Once this control has been given, the OS can then switch the processor to working on another process.

With faster CPUs, this gives the impression that several processes are running **at the same time** - a process known as **Concurrency.** It should, however, be noted that no matter the speed of the processor, only **one instruction per physical core** is executed at any given time.

## Process Scheduling

The scheduler is the component of an operating system which **decides which processes the CPU should work on next.** it works as follows:

- If the current process still remains the highest-priority task, **return its control of the CPU.** Otherwise:
	- **Save** the process' state in the process table
	- **Retrieve** the state of the newly highest-priority process
	- **Transfer control of the CPU** to this new process, **beginning** from the point indicated by the **Program Counter.**

This procedure of saving the current process and switching to another is known as a **context switch.** It **causes overhead** and thus its use must be **minimized where possible.**

Scheduling itself involves determining **optimal order and timing** of assigning **execution time to processes.** It does this via various scheduling criteria, including:
- **CPU utilisation** - the intent is to keep the CPU **as busy as possible** to minimize idle time.
- **Efficiency** to maximise system throughput, in accordance with the above.
- **Fairness** to all current users of the system - one should not be prioritised over another.

This results in different **methods** of scheduling.

### Scheduling Policies and Algorithms

There are **two scheduling policies:**
- **Non-preemptive,** where processes are run until complete or forced to wait for I/O
- **Preemptive,** where processes can be interrupted and replaced by others, generally via **timer interrupts**

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

## Threads
Threads are **independent paths/sequences** of execution within a process. Process are run with a **single execution thread by default.**

In some cases, parts of a process can be **parallelised** to increase efficiency/usability - this is known as **multi-threading,** and generally is a method to improve application performance.

### Differences between Threads and Processes
Both have some **shared features:**
- Single sequential **flow of control** with **start and end**
- At anytime, threads have a single **point of execution**
- Threads contain their own Thread Control Block (**TCB**), similar to a PCB
- Three-state model:  **RUNNING, BLOCKED, READY**
- Context switching
- Threads can spawn child threads, same as processes

For this reason, threads are sometimes called **lightweight processes.**

Threads have some important **differences:**
- Threads **cannot exist on their own - only within a process**
- Typically **created/controlled**  by an existing process
- Can **share properties with a process** such as memory and open files
- Creating them and switching with them is **inexpensive** as they **don't require separate address spaces**

Multiple threads can be compared with running multiple processes, but **threads share address space** where **processes share resources** (such as memory, I/O, etc.)

To simplify, threads **share process properties, but have their own private block of properties as well** - This is visualised below: 
![[ProcessThreadBlock.png]]

### Sequential and Concurrent Programming

#### Sequential Programming

Sequential programming refers to **constructing a program using a sequential language**, where the assumption is made that statements are **executed in order, on a single-CPU system.**

As a result, we can say that they use a **single thread** of control.

#### Concurrent Programming

Concurrent programming takes advantage of the concurrency that is allowed by using **multiple threads.** This allows the process to perform **parallel computations** and control several external activities **simultaneously.**

Concurrent programs can run on **both** multi and single-CPU systems. This is referred to as **true parallelism** and **multitasking** respectively.

However they require support from both the **programming language** and **OS.** generally this is **not a problem on modern OSes** as almost all of them support multithreading.

### Sequential and Concurrent Execution

#### Sequential Execution
##### Order and Precedence
In sequential programs, there is only ever **one possible execution sequence,** as the program dictates as such to the system. 

For example, in a program with three statements - **P, Q & R,** the program is executed in exact order of definition (i.e. **P => Q => R**).

This can be represented from two perspectives; **High** and **System** level.

###### High-Level

```
x = 1;		//P
y = x+1;	//Q
x = y+2;	//R

/* The final values of x and y depend on the order in which these statements are executed */
```

###### System-Level

Statements are compiled into several machine instructions. An abstraction of it is as follows:
1) P is treated as a singular instruction:
	`P1`. store `1` at address of `x`
2) Q is broken into 3 machine instructions:
	`Q1`. load value `x` into CPU register
	`Q2`. increment value of this register by `1`
	`Q3`. store value in this register at address of `y`
3) R is also broken into 3 machine instructions:
	`R1`. load value `y` into CPU register
	`R2`. increment value of this register by `2`
	`R3`. store result at address of `x`

##### Nature of Sequential Execution
The program-level execution sequence **P => Q => R** 
implies system-level sequence **P1 => Q1 => Q2 => Q3 => R1 => R2 => R3**

Single-threaded computation has no overlap in statement execution. This is known as **total ordering.**

Programs in this style are **deterministic,** meaning the same input always produces the same output, as a strict sequence of steps is specified.

This does not have many practical applications nowadays however, as proper sequencing is not really needed.

#### Concurrent Execution

##### Interleaving
In the below example, 10 different instances of interleaving are shown, yielding 10 different possible execution sequences.

![[Interleaving.png]]

A single run of a program corresponds to a single interleaving sequence, and each sequence determines a unique order of statement execution. 

Using a concurrent program with threads `t1` and `t2` as an example:

```
t1;
begin s1; ... sm; end;

t2;
begin p1; ...; pn; end;

begin t1, t2;
end;
```

The number of interleavings can be calculated with the following equation: 
$$\frac{(n+m)!}{n!m!}$$ 
This grows extremely quickly as *n* and *m* increase.

##### Thread Interference

Generally, concurrent execution is **non-deterministic** - the same input obtains a different output due to ordering. As an example:

A high-level program spawns two threads - `t1` and `t2`, that manipulate the same variable. The code is shown below:

![[RaceConditionsExample1.png]]

When we break the program down into a system-level process, one interleaving outcome is as follows:
1) `Thread t1: Retrieve c`
2) `Thread t2: Retrieve c`
3) `Thread t1: Increment retrieved value; result is 1`
4) `Thread t2: Decrement retrieved value; result is -1`

Since `t2` acted last, `t1`'s outcome is overwritten.

### User and Kernel Threads

#### User Threads
User threads are typically created and managed by a **user-level library, typically without kernel knowledge.** They are:
- Fast to create and manage
- Portable to any OS

However:
- If **one thread is blocked, all others are!**
	- For example, a word processor that uses a thread to print a document would hold up all other threads during the timeframe of its execution.

- Multi-threaded applications **cannot** take advantage of **parallel execution.**

#### Kernel Threads

Kernel threads are **Directly managed and supported by the kernel.** They effectively have the inverse properties of user threads:

- Slower to create and manage
- OS specific
- Another thread can be scheduled if one is blocked
- Parallel execution can be taken advantage of on multiple CPUs

### Multi-threading models

#### Multi-thread mapping

As stated before, kernels are generally **not aware of user threads** in a process. Therefore, **thread libraries** must manually map user threads to kernel threads.

This is done through many different methods, including:

##### Many-to-One
All user threads from each process are mapped to **one** kernel thread.

Pros:
- More portable - **few system dependenices**

Cons:
- **No parallel execution** of threads
- All threads in a process are **blocked when one waits**
		
##### One-to-One
**Each** user thread maps to a **single** kernel thread.

Pros:
- **Concurrency is possible** - if one thread is blocked, others are not
- Better multi-CPU performance

Cons:
- **Slow due to management overhead**
	- The kernel is involved in management of **every single user thread**
- **Restrictions on number of threads**
- Requires corresponding **kernel support**
	
##### Many-to-Many
In this, many user threads are multiplexed to many kernel threads **of an equal or smaller number.**

Pros:
- Can take advantage of **multiple CPUs**
- **No restrictions on thread numbers**
- When blocking, the kernel can schedule other threads.

Cons:
- **Difficulty of implementation** due to complexity.

### Inter-Process Synchronisation
#### As a solution to interleaving interference
Threads in a system behave in two ways dependant on situation:

- Threads can **compete** over resources or access to particular addresses, syscalls, etc...
- Or they can **cooperate** when the transit of information from one process to another is required.

OSes themselves contain threads which are constantly doing both. inter-process synchronisation acts as a solution that allows threads and processes to **share resources.**

#### Critical Section and Mutual Exclusion
A **critical section** in code is a process that involves either **sensitive operations** or a **shared resource.**

Competition for resources in these sections are referred to as **race conditions.** These are **unstable and therefore undesirable!** As a general rule, critical sections should only be enterable by **one thread at a time.** this is guaranteed through a process known as **mutual exclusion** - and is a major design issue in OSes.

##### Examples of Race Conditions

###### Example 1: Racing for memory access

![[RaceConditionsExample1.png]]

###### Example 2: Racing for peripherals
In this instance, two threads are competing for access to the printer spooler directory:

![[RaceConditonsExample2.jpg]]

1) Next available printer job slot: 7
2) A and B access simultaneously
3) A reads 7, timer interrupt, switch to B before A stores anything
4) B reads 7, stores job and increment vals
5) A switches back, stores job at 7

##### Mutual Exclusion on a Critical Section

![[MutualExclusion.jpg]]

Mutual exclusion is assured when **no two processes** are simultaneously inside their critical regions. To do this, the following must be observed:

- **No assumptions** may be made about **speed** or the **number of threads**
- **No process or thread running outside its critical region may block other processes**
- No process should have to **wait forever to enter its critical region**

#### Shared Resources
`NOTE: Critical Sections and semaphores can be scaled up to allow protection of shared resources in distributed systems - it will be looked at next term.`
##### Semaphores
Semaphores are data structures that allow the enforcement of mutual exclusion through a design similar to its railroad namesake; when a resource is in use, the Semaphore prevents use of it by others until it is free.

###### Example:
Semaphore *S* is an integer that only takes *non-negative* values. Only two indivisible operations on *S* are allowed: 

*Wait(S)* on the Non-critical section and *Signal(S)* on the critical section. They are defined as follows:
```
wait(S) {
	if (S > 0) S--;
}

signal(S) {
	S++;
}
```

*Wait* and *Signal* allow the processor to be switched from a blocked process/thread to another process/thread (a **context switch**).

#### The Producer-Consumer Problem

![[ProcConsumeProb.png]]

This describes a programming issue where a producer repeatedly produces items, placing them into a buffer, and a consumer takes items one-by-one from the buffer. A few assumptions are made:

- First In First Out (FIFO) buffering is used
- Producers can produce new items at any time, but the **buffer cannot be full**
- The consumer can consume an item from the buffer **only if it is not empty**
- The program terminates when all items produced are eventually consumed.

##### The naive solution

The number of items can be kept track of through use of interleaving:

```
Producer Class:

loop {
		Produce item i;
		if(itemCount == N){
			sleep(producer);
		}
		Put item i;
		itemCount++;
		if(itemCount == 1){
			wakeup(consumer);
		}
}

Consumer Class:

loop {
		if(itemCount == 0){
			sleep(consumer);
		}
		Remove item j;
		itemCount--;
		if(itemCount == N - 1){
			wakeup(producer);
		}
		Consume item j;
}

```

Interleaving in this instance, however, can cause a race condition - and could lead to a *deadlock*.

###### Deadlocks

Deadlocks occur when two or more threads are waiting for each other to finish. To be exact, four conditions must hold simultaneously for one to occur:

1. **Mutual Exclusion** - a resource can be assigned to at most *one* process at a time.
2. **Hold and wait** - processes holding resources are allowed to request and wait for additional resources
3. **No preemption** - resources that have previously locked cannot be forcefully unlocked by another process; they must be released by the process holding the resource.
4. **Circular wait** - There must be a chain of processes, such that each member of a chain is waiting for a resource held by the next member of the chain.

![[CircularWait.png]]

###### Example of a Deadlock in The Producer-Consumer Problem

One possible deadlock scenarios occurs as follows, using the code shown earlier:

1. A consumer reads itemCount  = 0, so it needs to call sleep(consumer).
2. Just before calling sleep(), the consumer is interrupted (timer interrupt) and the producer resumes.
3. The producer adds an item to the buffer - so itemCount = 1 now.
4. Producer tries to wakeup(consumer), but consumer is already awake, so the call is missed.
5. When the consumer resumes, sleep(consumer) is called, forcing the thread to sleep.
6. The producer continues to add items to the buffer until it is full; at which point it calls sleep(producer), causing its own thread to sleep.
7. As both processes have slept waiting to be woken by the other, no progress can be made and a deadlock has occurred.

##### Solving the Producer-Consumer problem using semaphores.

With the following code:

```
ItemsReady = 0
SpacesLeft = N // Size of Buffer

Producer Class:

loop {
	Produce item i
	Wait(SpacesLeft) //decrement
	Put item i
	Signal(ItemsReady) //increment
	}

Consumer Class:

loop {
	Wait(ItemsReady) //decrement
	Get item i
	Signal(SpacesLeft) //increment
	Consume item i
	}
```

When semaphores are used correctly, $N = SpacesLeft + ItemsReady$.

##### Multiple Producers-Consumers Problem

![[MultiProcConsumeProb.png]]

The prior solution only works well when a single producer and consumer are present. When we have multiple, a race condition is caused.

###### Using Semaphores (Again)

For multiple producers and consumers, we include an additional semaphore to satisfy Mutual Exclusion, known as a *mutex* or *binary semaphore*. It is a semaphore that can only be released by its owner.

```
Producer Class:

loop {
	Produce item i
	Wait(SpacesLeft)
	Wait(BusyBuffer) //mutex
	Put item i
	Signal(BusyBuffer)
	Signal(ItemsReady)
	}
	
Consumer Class:

loop {
	Wait(ItemsReady)
	Wait(BusyBuffer) //mutex
	Get item i
	Signal(BusyBuffer)
	Signal(SpacesLeft)
	Consume item i
	}
```

$BusyBuffer$ has ownership, meaning that it can only be increased/decreased by the same process. It initially is set to a value of 1.

It should be noted that the *order in which* semaphores or incremented/decremented is essential.

#### The Dining Philosophers Problem

![[DiningPhilosophersProb.png]]

This problem describes 5 philosophers sat around a table eating and thinking. Each has a plate of spaghetti that can be eaten with forks. The requirements are as such:

- Philosophers can only eat and think
- Between each pair of plates is one fork
- Each philosopher needs *two forks* to eat spaghetti
- No two philosophers can hold the same fork at once.

##### Using Semaphores

![[DiningPhiloSemaphores.png]]

In this scenario, each philosopher is a different thread with a unique ID, and there is one semaphore per fork/chopstick. Left and right chopsticks are identified using the ID of the philosopher; `left = chopstick[i]`, `right = chopstick[((i-1)+N)%N]`.

```
Philosopher Class (int i)

// i is the id of the philosopher

loop {
	think();
	wait(chopstick[left]); //take left
	wait(chopstick[right]); //take right
	eat();
	signal(chopstick[left]); //release left
	signal(chopstick[right]); //release right
}
```

With this solution, no chopstick is ever held by two philosophers. However, there is a scenario where a deadlock can occur:

Suppose that all five philosophers want to eat at the same time, so they all take their left chopsticks:

1. Phil 0 takes `chopstick[left]`
2. Phil 1 takes `chopstick[left]`
3. Phil 2 takes `chopstick[left]`
4. Phil 3 takes `chopstick[left]`
5. Phil 4 takes `chopstick[left]`

With this, a circular wait has occured, causing a deadlock.

The solution, again, is to add an additional semaphore to act as a mutex:

```
Philosopher Class (int i):
	loop {
		think();
		wait(busy); //mutex
		wait(chopstick[left]); //take left
		wait(chopstick[right]); //take right
		eat();
		signal(chopstick[left]); //release left
		signal(chopstick[right]); //release right
		signal(busy); //release mutex
	}
```

This resolves the deadlock entirely.