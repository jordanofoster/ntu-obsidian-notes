#comp20111-dnaos/topic-2 
# Inter-Process Synchronization

In a typical system, [[Threads|threads]] work in one of two ways:
1) *Compete* over resources/access to [[memory addresses|addresses]], syscalls, etc.
2) *Cooperate* when moving information between [[Processes|processes]].

OSes contains threads that do both. 

Inter-process synchronization allows [[Threads|threads]] and [[Processes|processes]] to share resources.

## Critical Sections and Mutual Exclusion

A *critical section* is a [[Processes|process]] in code that involves *sensitive operations* on a 