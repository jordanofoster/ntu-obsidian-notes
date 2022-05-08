#comp20111-dnaos/topic-2 
# Inter-Process Synchronization

In a typical system, [[Threads|threads]] work in one of two ways:
1) *Compete* over resources/access to [[memory addresses|addresses]], syscalls, etc.
2) *Cooperate* when moving information between [[Processes|processes]].

OSes contains threads that do both. 

Inter-process synchronization allows [[Threads|threads]] and [[Processes|processes]] to share resources.

## Critical Sections

A *critical section* is a [[Processes|process]] in code that involves *sensitive operations* on a *shared resource.* Competition in them cause *[[Inter-Process Synchronization#Race Condition|race conditions]]*.
	- These are **unstable and undesirable.** 
		- To fix this, only one [[Threads|thread]] should be able to enter a section at a time.
			- This is achieved through *Mutual Exclusion.*

## Mutual Exclusion

*Mutual Exclusion* is assured when *no two [[Processes|processes]]* are simultaneously inside their own [[Inter-Process Synchronization#Critical Sections|critical regions]]. 