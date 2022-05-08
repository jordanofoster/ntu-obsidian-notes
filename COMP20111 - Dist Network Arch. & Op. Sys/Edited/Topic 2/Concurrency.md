#comp20111-dnaos/topic-2
# Concurrency

- CPUs only execute [[Processes#Process States|one]] instruction at a time.
- Work continues on a process until:
	- [[Interrupts#Interrupt Handling|I/O request]] via syscall
	- [[Interrupts|Interrupt]] 

- Some CPUs can switch processes so fast that concurrent execution *seems* to occur.
	- [[Fetch-Execute Cycle|Only one instruction]] *per physical core*/CPU is ever executed.