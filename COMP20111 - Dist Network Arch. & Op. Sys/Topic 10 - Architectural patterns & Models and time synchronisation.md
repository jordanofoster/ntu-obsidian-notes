# Architectural patterns & Models and time synchronisation

## Architectural patterns

There are a number of ways for information and remote invocation to take place, and these usually form the basis of software behind a distributed system. There are numerous types of approaches:
- Layering
![[Pasted image 20220314131123.png]]
- Tiered
![[Pasted image 20220314131208.png]]
- Pattern based
	- Model View Controller (MVC)
![[Pasted image 20220314131311.png]]
- Proxy
![[Pasted image 20220314131706.png]]
- Broker
![[Pasted image 20220314131448.png]]
- Middlewares (from [[Topic 8 - Messaging Systems|Topic 8]])
![[Pasted image 20220314131726.png]]

## Fundamental Models
Each form of architectural model uses a set of fundamental concepts:

### Interaction Model
![[Pasted image 20220314132231.png]]
When thinking about multiple servers and clients, different programs/services work together to provide overall functionality. How the distributed algorithms work requires consideration, alongside the interactions between each party. In interaction models:

- Multiple machines interact with eachother to perform some system function.
- A distributed algorithm allows messages to be passed between components of the distributed system.
- Communication performance must be considered:
	- Latency
	- Bandwidth
	- Jitter
- Clocks and timing issues also factor into performance.
- Interaction models can be synchronous or asynchronous.

### Failure Model
Failure models let you consider how they occur and how best to understand and correct them; failure handling itself has already been introduced in [[Topic 7 - Distributed Computing & Challenges#Failure Handling|Topic 7.]] There ar ea few types of failures:

- Omission failures
	- Process omissions
	- Communication omissions
- Arbitrary failures (or *Byzantine* failures)
- Timing failures
	- These differ depending on whether the system is synchronous or not:
		- Synchronous systems can suffer from failures in the following areas:
			- Clock drift
			- Message delivery time
			- Process execution timing
		- Asynchronous systems generally may face errors related to taking *too much* time to do something, but generally do not face timing errors.

When failures occur, we can adopt 
### Security Model
With multiple components together, these model how we protect or secure objects, components and processes from attack.

