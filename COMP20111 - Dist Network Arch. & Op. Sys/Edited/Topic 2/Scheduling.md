# Scheduling

- Schedulers decide which [[Processes|processes]] should be worked on next by the CPU.
- Changes made via a *[[Scheduling#Context Switch|context switch]]*

## Context Switching

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
- **Non-Preemptive**
	- Processes run until complete, or **[[Processes#^1436ce|BLOCKED]]** 
- **Preemptive**
	- Processes interrupted and replaced by others
		- Generally on a [[Interrupts#^46cbff|timer]].

*Six* major policies covered:

### Non-Preemptive Algorithms

- [[First Come, First Serve (FCFS) or First In, First Out (FIFO)]]
- [[Shortest Job First (SJF)]]

### Preemptive Algorithms

- [[Shortest Remaining Time (SRT)]]
- [[Highest Response Ratio Next (HRRN)]]
- [[Round Robin (RR)]]
- [[Multi-Level Feedback Queues (MFQ)]]