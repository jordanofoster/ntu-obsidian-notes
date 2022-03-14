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
![[Pasted image 20220314132622.png]]

Failure models let you consider how they occur and how best to understand and correct them; failure handling itself has already been introduced in [[Topic 7 - Distributed Computing & Challenges#Failure Handling|Topic 7.]] There are a few types of failures:

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

When failures occur, we can either hide them, or make the effects of the failure less severe.

### Security Model
![[Pasted image 20220314132702.png]]
With multiple components together, these model how we protect or secure objects, components and processes from attack. We need to consider how to secure running systems, as well as the methods by which they communicate with eachother. There are two ways of doing this:
- Protecting remote objects
- Security interactions themselves

There are a few security concerns for distributed systems:
- Securing remote method invocations
	- How do we know that a device that calls a method is the device it claims to be?
- Other threats:
	- [Man-in-the-middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)
	- [Denial-of-service attacks](https://en.wikipedia.org/wiki/Denial-of-service_attack)
	- [Mobile code](https://en.wikipedia.org/wiki/Code_mobility) - as covered in lab 5
- The situation can be improved via secure communications:
	- We can use cryptography to encrypt message details.
	- We can verify the identity of an authenticated user by applying their private key to encrypted messages.
	- Securely encrypted channels.

## Revisiting Cluster Computing
![[Pasted image 20220314133329.png]]
There are a few issues that need to be addressed for any large-scale distributed system:
- Networking
- Tranmission of information
- Clocks
- States
- Synchronisation
- Scheduling
- Load Blanacing
- Remote Invocation / IPC
- Distributed Memory
- Distributed Filesystems
- Security

## Revisiting Multi-computer Topologies
![[Pasted image 20220314133503.png]]

Multi-computers can be connected via a number of ways. There are some things to consider:
- Nodes in topologies represent switches, with CPUs connected to switches.
- Each node can have a number of links to other nodes (fanout).
- The diameter of an interconnection network represents the largest number of links that may need to be traversed between the two most distant nodes. The lowest number of hops is the best, and is known as the shortest path.
- Maximum bandwidth between nodes.

### Sender/receiver initiated Diffusion
![[Pasted image 20220314133800.png]]
![[Pasted image 20220314133807.png]]
One issue with large-scale computing is transmitting workload between nodes via different load balancing strategem. Some common ones include the namesakes of this section. Load balancing is covered in [[Topic 9.]]

## Clocks in distributed systems
Time is an important notion with distributed systems; when sending information between interconnected nodes, we must consider the order that messages are processed/distributed in. Processes running on two or more machines can use the clock to timestamp events and keep track of synchronisation.

### Clock issues in the Interaction Model
![[Pasted image 20220314133957.png]]
![[Pasted image 20220314134003.png]]

When different programs and/or services work together to provide overall system functionality across a number of machines, how our distributed algorithms work and the interactions between each computer needs to be considered, including:

- Performance considerations such as latency/bandwidth/jitter
	- This also means we must consider clocks and how they relate to the interaction model.
- Clocks & Timers
	- Each machine in a distributed system has its own internal clock.
	- Clocks & Timers are used within the OS for pre-emptive multitasking (when considering a singular machine).
	- In distributed systems, processes running on two or more machines can use the clock to timestamp events and track synchronisation.

### Clock Skew and Drift
![[Pasted image 20220314134345.png]]
Each node on the network has its own internal clock. In the example above, two nodes have the same time, but $c_2$ is out by a minute.
- There is *no difference* between $c_1$ and $c_3$ 
- There is a difference of *1 minute* between $c_1$ and $c_2$.
- This difference is called *skew* (i.e. the difference between two readings).

System clocks are based on a timing circuit which oscillates $x$ times/second. For example, a 2.4GHz processor oscillates 2.4 billion times/second. There can be *slight differences* between circuits in different nodes:
- For example, one may do $2,400,000,000$ oscillations where another does $2,400,000,001$ due to a variety of reasons, such as current crystal temperature.
	- This is known as *clock drift.*

### Strategies to synchronise physical clocks
There are various:
- External Synchronisation
	- An external source synchronises each individual clock with the correct time.
- Internal Synchronisation
	- Each individual clock is synchronised with eachother to a known accuracy (bound), then the interval between two events occuring on different machines can be measured.

There are various other things to consider regarding clocks:
- Correctness
- Monotonicity
- Faultiness (crash/arbitrary failures)

#### [Cristian's Algorithm](https://en.wikipedia.org/wiki/Cristian%27s_algorithm)
![[Pasted image 20220314135311.png]]
Proposed in 1989 by [Flaviu Cristian](https://en.wikipedia.org/wiki/Flaviu_Cristian) - who came up with a probabilistic algorithm to set clocks within an intranet to an external time source (*external synchronisation*).

#### [The Berkeley Algorithm](https://en.wikipedia.org/wiki/Berkeley_algorithm)
Introduced by Gusella, R., and Zatti, S. in 1989, this algorithm syncs clocks using a server/client polling method, a la *internal synchronisation.*

![[Pasted image 20220314135658.png]]

![[Pasted image 20220314135736.png]]

#### The Network Time Protocol
Both Cristian's and the Berkley algorithm are intended for local network use; the Network Time Protocol (NTP) is used for clock synchronisation over a WAN or the internet (made of many WANs). Its design aims are as follows:
- *"To provide a service enabling clients across the Internet to be synchronised accurately to UTC"*
- *"To provide a reliable service that can survive lengthy losses of connectivity"*
- *"To enable clients to resynchronise sufficiently frequently to offset the rates of drift found in most computers"*
- *"To provide protection against interference with the time service, whether malicious or accidental"*
![[Pasted image 20220314152328.png]]
Servers are connected in a logical hierarchical tree, called a synchronisation subnet. Each level/strata of the tree contains servers:
- At the top-most stratum are primary servers, the next secondary, and so on;
	- The bottom stratum deals with user machine clocks.
- Timing information is passed through each strata.

