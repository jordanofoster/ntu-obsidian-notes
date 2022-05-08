# Multithreading

Multithreading refers to the *[parallelization](https://en.wikipedia.org/wiki/Parallel_computing)* of a [[Processes|process]]. This generally *improves* application performance in the form of efficiency and/or usability.

## Multithreading Models

There are several strategies - or models - to facilitate multithreading.

### Multithread Mapping

This refers to mapping a [[Threads#User Threads|user thread]] to a [[Threads#Kernel Threads|kernel thread]], to mitigate various shortcomings of the former. There are several methods:

#### Many-To-One

- All [[Threads#User Threads|user threads]] in a [[Processes|process]] are mapped to *one* [[Threads#Kernel Threads|kernel thread]].
	- More portable (*fewer system dependencies*)
	- *No* [[Programs#Concurrent Program Execution|concurrent execution]] of threads.
	- blocking issues, [[Threads#^5bfc61|like in user threads]].

#### One-To-One

- Each [[Threads#User Threads|user thread]] maps to *one* [[Threads#Kernel Threads|kernel thread]].
	- [[Programs#Concurrent Program Execution|Concurrent execution]] possible
		- Due to [[Threads#^efd154|independent threads]]
		- 