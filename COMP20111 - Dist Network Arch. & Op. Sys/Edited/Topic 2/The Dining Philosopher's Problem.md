#comp20111-dnaos/topic-2 
# The Dining Philosopher's Problem

![[DiningPhilosophersProb.png]]

5 philosophers are sat around a table, eating and thinking. Each has a plate of spaghetti, eaten with forks. The following is observed:

- Philosophers can only *eat* and *think*
- A *fork* is between each *pair of plates*
	- Each philosopher requires *two forks* to *eat*
	- No two philosophers can *share the same fork.*

## Using [[Shared Resources#Semaphores|Semaphores]]

![[DiningPhiloSemaphores.png]] ^a1b0b4

Here, we each philosopher is modelled as a [[Threads|thread]] with a [[Processes#^a534ab|unique ID]] - there is one [[Shared Resources#Semaphores|Semaphore]] per *chopstick/fork*.

Left/Right chopsticks are identified using the *philosopher's ID*:
`left = chopstick[i]`
`right = chopstick[((i - 1) + N)%N]`

Our *Philosopher* class is as follows:
```
Philosopher Class (int i)

// i is the id of the philosopher

loop {
	think();
	wait(chopstick[left]); //take left
	wait(chopstick[right]); //take right
	eat();
	signal(chopstick[left]); //release left
	signal(chopstick[right]); //release right
}
```

With this method, no chopstick is ever held by two philosophers. A [[Deadlocks|deadlock]] can still occur, however:

![[Deadlocks#Example of a Deadlock in The Dining Philosopher's Problem]]


Our solution is the [[The Producer-Consumer Problem#^e0635b|same]] as with *[[The Producer-Consumer Problem#Multiple Producers-Consumers Problem|The Multiple Producers-Consumers Problem]]* - we use a *mutex* [[Shared Resources#Semaphores|semaphore]]:

```
Philosopher Class (int i):
	loop {
		think();
		wait(busy); //mutex
		wait(chopstick[left]); //take left
		wait(chopstick[right]); //take right
		eat();
		signal(chopstick[left]); //release left
		signal(chopstick[right]); //release right
		signal(busy); //release mutex
	}
```

