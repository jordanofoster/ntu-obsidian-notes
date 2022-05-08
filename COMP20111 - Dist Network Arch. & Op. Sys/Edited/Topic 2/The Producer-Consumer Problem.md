# The Producer-Consumer Problem

This is a programming issue where a producer *produces* items, putting them in a buffer, and a *consumer* takes items *one-by-one* from that same buffer.

![[ProcConsumeProb.png]]

Some assumptions are made:

1) [[First Come, First Serve (FCFS) or First In, First Out (FIFO)|FIFO]] buffering is used
2) Producers can make new items at any time...
	- But the buffer **cannot be full**
3) Consumers can take items from the buffer...
	- But only if it **is not empty**
4) The program terminates when all produced items are consumed.

## The naïve solution

The number of items can be kept track of through use of [[Interleaving|interleaving]]:

```
Producer Class:

loop {
		Produce item i;
		if(itemCount == N){
			sleep(producer);
		}
		Put item i;
		itemCount++;
		if(itemCount == 1){
			wakeup(consumer);
		}
}

Consumer Class:

loop {
		if(itemCount == 0){
			sleep(consumer);
		}
		Remove item j;
		itemCount--;
		if(itemCount == N - 1){
			wakeup(producer);
		}
		Consume item j;
}

```

^445f51

In this instance it can cause a [[Race Conditions|race condition]] - and could lead to a *[[Deadlocks|deadlock]]* - see below:

![[Deadlocks#Example of a Deadlock in The Producer-Consumer Problem]]
