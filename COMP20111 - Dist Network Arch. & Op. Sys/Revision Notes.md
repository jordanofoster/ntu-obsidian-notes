# Term 1
## Operating Systems
### OS Structure
- Collections of programs
	- Manage hardware resources, I/O
		- Machine extending - abstraction of hardware issues from user

- Provide:
	- Concurrency
	- Shareable resources (RAM, CPU, etc)
	- Long-term storage access (hard drives, SSDs, etc)
	- Non-determinacy
		- Resiliency to unpredicted events (i.e. not crashing)

- 
### File Systems

## Concurrency
### Process Life Cycle
- One of two methods:
	- Explicitly executed by user
	- Child spawned by parent process - spawning/forking
		- Child can spawn own processes - makes tree.

### State Queues
- Three states:
	- **RUNNING**
		- One process at a time
	- **READY**
		- In queue of other **READY** processes
	- **BLOCKED**
		- In queue related to blocked resource

### Process Termination
- Voluntarily:
	- **Normal** - process finishes
	- **Error** - through inbuilt error handling
- Involuntarily:
	- **Fatal error** - OS detected
	- **Killed** - by other process, via syscall.

### Process Execution
Process starts -> \[LOOP\] Fetch Instruction -> Decode -> Execute \[END LOOP\]-> Process ends

- Cycle **broken when:**
	- **BLOCKED** cannot be dealt with
	- **High priority interrupt**

### Interrupts
1) Interrupt Received
2) current process suspended; handles Interrupt Service Routine (*ISR*)
3) Suspended process resumes

- **Three types:**
	- **I/O** - signals completion/error
	- **Timer** - set interval/time
	- **Program** - via error

**Main way OSs multitask.**

### Process Scheduling

- Scheduler: Decides what processes CPU does next.

- If current process not highest-priority:
	1) Save state in process table
	2) Retrieve highest-prio process state
	3) Transfer cpu control, beginning from Program Counter point

1-3 is a *context switch*. Causes o


## Memory Management

## I/O

## File Systems

# Terms 2/3

## Distributed Computing

## Java

## Challenges in Distributed Systems

## Messaging Systems

## Coordination

## Scheduling

## Other Distributed Computing

## Architectural Patterns & Models

## Clocks & Synchronization

## Virtualization & Cloud