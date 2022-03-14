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
When thinking about multiple servers and clients, different programs/services work together to provide overall functionality. How the distributed algorithms work requires consideration, alongside the interactions between each party.

In Interaction Models, multiple machines interact with eachother to perform some s

### Failure Model
Failure models let you consider how they occur and how best to understand and correct them.

### Security Model
With multiple components together, these model how we protect or secure objects, components and processes from attack.

