# Shared Resources

## Semaphores

Semaphores are *data structures* that allow [[Inter-Process Synchronization#Mutual Exclusion|Mutual Exclusion]] to be enforced. When a resource is in use, they prevent other [[Threads|threads]]/[[Processes|processes]] from using it until free.

### Example:

Semaphore $S$ is an integer that only takes *non-negative* values. Only two indivisible operations on $S$ are allowed:
- `Wait(S)` - on the *non-critical* section
	```
	wait (S) {
		if (S > 0) S--;
	}
	```
- `Signal(S)` - on the *[[Inter-Process Synchronization#Critical Sections|critical section]]* 
```
Signal(S) {
	S++;
}
```

Both 