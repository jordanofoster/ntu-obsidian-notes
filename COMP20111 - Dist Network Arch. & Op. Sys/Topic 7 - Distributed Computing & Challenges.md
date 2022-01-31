# Distributed Computing & Challenges

## Current computing paradigms

Generally, computers are thought of as single devices, as seen below:

![[Pasted image 20220131131304.png]]

Everyday devices fall under the *centralized* computing paradigm. This means that for each device, they have a local set of resources (memory, processor, I/O, graphics, storage). They are fully shared and tightly coupled, with unification achieved under one operating system.

## What is parallel computing?

In parallel computing, all processing nodes in a machine can be coupled in different ways; tightly coupled, with shared memory, or loosely coupled, with distributed memory (or clusters), as shown below:

![[Pasted image 20220131131904.png]]

### Distributed Computing

Distributed systems are made up from multiple autonomous computers; each has its own CPU and memory, and communication is done through a network. *Message passing* is used to exchange information - depending on topology and use, a distributed system could be used to form a cluster (*highly-coupled*) or cloud (*highly/loosely-coupled*); the latter can be centralised or distributed depending on purpose.

#### Trends in Distributed SYs

