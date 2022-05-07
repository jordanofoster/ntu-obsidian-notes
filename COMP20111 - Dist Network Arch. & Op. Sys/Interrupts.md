# Interrupts

Signals sent to CPU that require **immediate attention.** indicates hardware/software event. Construct that allows [[Concurrency|multitasking]] to occur.


## Interrupt Handling

Using an I/O blocking event as an example:

1) Event occurs. Process execution **suspended.**
2) CPU begins work on **another process.**
	1) Former process goes from **[[Processes#^1436ce|BLOCKED]]** to **[[Processes#^555d69|RUNNING]]** - sends interrupt to CPU
	2) CPU handles **[[Interrupt Service Routine (ISR)s|Interrupt Service Routine (ISR)]]**
3) Former process *resumed.*

## Interrupt Types

Many types; three examples:
- **I/O Interrupts**
	- Signal from I/O device, completion or error.
- **Timer Interrupts**
	- Caused by processer timer, alerting OS at intervals.
- **Program Interrupts**
	- [[Processes#Process Termination|Errors,]] both fatal and non-fatal.