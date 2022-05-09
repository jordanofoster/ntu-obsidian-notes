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

## Solving [[The Producer-Consumer Problem]] using [[Shared Resources#Semaphores|Semaphores]]

We do so with the following code:
```
ItemsReady = 0
SpacesLeft = N // Size of Buffer

Producer Class:

loop {
	Produce item i
	Wait(SpacesLeft) //decrement
	Put item i
	Signal(ItemsReady) //increment
	}

Consumer Class:

loop {
	Wait(ItemsReady) //decrement
	Get item i
	Signal(SpacesLeft) //increment
	Consume item i
	}
```

When our semaphores are used correctly, $N =$ `SpacesLeft` $+$ `ItemsReady`.

# Multiple Producers-Consumers Problem

![[MultiProcConsumeProb.png]]

Our [[The Producer-Consumer Problem#Solving The Producer-Consumer Problem using Shared Resources Semaphores Semaphores|prior solution]] only works well when a *single* producer-consumer pair is present. With more, we once again get [[Race Conditions|race conditions]].

## Solving [[The Producer-Consumer Problem#Multiple Producers-Consumers Problem|The Multiple Producers-Consumers Problem]] using [[Shared Resources#Semaphores|Semaphores]]

To ensure [[Inter-Process Synchronization#Mutual Exclusion|mutual exclusion]] across multiple producers and consumers, we include a *mutex/binary* [[Shared Resources#Semaphores|semaphore]] - that can only be released by its *owner.*

```
Producer Class:

loop {
	Produce item i
	Wait(SpacesLeft)
	Wait(BusyBuffer) //mutex
	Put item i
	Signal(BusyBuffer)
	Signal(ItemsReady)
	}
	
Consumer Class:

loop {
	Wait(ItemsReady)
	Wait(BusyBuffer) //mutex
	Get item i
	Signal(BusyBuffer)
	Signal(SpacesLeft)
	Consume item i
	}
```

Here, `BusyBuffer`
