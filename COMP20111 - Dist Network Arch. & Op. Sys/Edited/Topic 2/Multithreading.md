# Multithreading

Multithreading refers to the *[parallelization](https://en.wikipedia.org/wiki/Parallel_computing)* of a [[Processes|process]]. This generally *improves* application performance in the form of efficiency and/or usability.

## Multithreading Models

There are several strategies - or models - to facilitate multithreading.

### Multithread Mapping

This refers to mapping a [[Threads#User Threads|user thread]] to a [[Threads#Kernel Threads|kernel thread]], to mitigate various shortcomings of the former. There are several methods:

#### Many-To-One

- All [[Threads#User Threads|user threads]] in a [[Processes|process]] are mapped to *one* [[Threads#Kernel Threads|kernel thread]].
	- M