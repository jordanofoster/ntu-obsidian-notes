# Deadlocks

These occur when *two or more* [[Threads|threads]] are waiting upon each other. More accurately, four conditions must hold simultaneously:

1) **[[Inter-Process Synchronization#Mutual Exclusion|Mutual Exclusion]]** 
	- The resource is assigned to *one* [[Processes|process]] at a time.
2) **Hold and Wait** 
	- [[Processes]] holding resources can request and wait for additional resources
3) **No Preemption** 
	- Previously-locked resources cannot be forcefully unlocked by another [[Processes|process]]
		- They must be *released* by the holding process.
4) **Circular Wait** ^5cb177
	- There must be a chain of processes - such that *each member* of a chain waits on a resource held by the *next member* in that chain.
	>![[CircularWait.png]]

## Example of a Deadlock in [[The Producer-Consumer Problem]]

This can occur as follows, using our [[The Producer-Consumer Problem#^445f51|previous code]]:

1) A consumer reads `itemCount = 0`, and therefore calls `sleep(consumer)`.
2) Just before calling `sleep()`, the consumer is [[Interrupts#^46cbff|interrupted]]; the *producer* wakes.
3) The producer adds an item to the buffer.
	- Now, `itemCount = 1`
4) Producer tries to call `wakeup(consumer)`
	- Consumer is already awake - call is missed.
5) Consumer resumes and calls `sleep(consumer)` as it was about to do.
6) Producer continues to add items to the buffer.
	- No consumer to take them, so it becomes full!
	- Producer calls `sleep(producer)` when this happens.
7) Both *consumer* and *producer* are asleep, and waiting to be awoken by the other.
	- No progress can be made; **[[Deadlocks|deadlock]]** occurs.

## Example of a Deadlock in [[The Dining Philosopher's Problem]]

A [[Deadlocks|deadlock]] can occur if *[[The Dining Philosopher's Problem#^a1b0b4|all five philosophers]]* want to *eat at once:*

1) Phil 0 takes `chopstick[left]`
2) Phil 1 takes `chopstick[left]`
3) Phil 2 takes `chopstick[left]`
4) Phil 3 takes `chopstick[left]`
5) Phil 4 takes `chopstick[left]`

A [[Deadlocks#^5cb177|circular wait]] has occurred; with this, all *four* conditions are held.