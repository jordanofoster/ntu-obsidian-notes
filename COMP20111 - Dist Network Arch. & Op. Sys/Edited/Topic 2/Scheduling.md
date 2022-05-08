#comp20111-dnaos/topic-2
# Scheduling

- Schedulers decide which [[Processes|processes]] should be worked on next by the CPU.
- Changes made via a *[[Scheduling#Context Switching|context switch]].*

## Context Switching

Context switching can be performed on both [[Processes|processes]] and [[Threads|threads]].

- If current process *not* highest priority:
	1) **Save** process [[Processes#Process States|state]] in [[Processes#Process Tables|table]]
	2) **Retrieve** state of new highest-priority process
	3) Begin/Resume process, as indicated by program counter.

- **Causes overhead** - should be minimized.

## Prioritization Metrics

^be213a

- Scheduling involves determination of *optimal order/timing* when assigning *execution time* to processes.
- Various metrics:
	- **CPU utilisation** ^c89b45
		- Keep it as **busy as possible**
	- **Efficiency**
		- Maximize throughput in accordance with [[Scheduling#^c89b45|the above]]
	- **Fairness** ^7ea821
		- Do not prioritize one user over another

## Scheduling Policies and Algorithms

Two policy types:
- **[[Non-Preemptive Algorithms]]**
	- Processes run until complete, or **[[Processes#^1436ce|BLOCKED]]** 
- **[[Preemptive Algorithms]]**
	- Processes interrupted and replaced by others
		- Generally on a [[Interrupts#^46cbff|timer]].

# Scheduling in Distributed Systems

Scheduling in distributed systems is a problem of *routing* - and ensuring that no nodes are *over/underloaded.*

There are a number of methods:
- [[Round Robin (RR)]]
- [[Weighted Round Robin (WRR)]]
- [[Sender/Receiver Initiated]]
- [[Least Connection/Least Loaded (LC/LL)]]
- [[Min-min]]
- [[Max-min]]
- [[Opportunistic Load Balancing]]
- [[Equally Spread Current Execution (ESCE)]]
- [[Throttled Load Balancing]]
- [[Ant Colony Optimisation]]