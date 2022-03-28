# Co-ordination, Scheduling and Resource Management

## Why do we need it?
**Coordination** is required so that a master coordinates activities within a cluster or system; any node can be the coordinator.

**Synchronisation** is needed because shared resources can be used. As a result, policies for dealing with distributed mutual exclusion is required.

**Scheduling**/load balancing methods are needed for dealing with workloads on individual nodes.

There are two types of algorithms for synchronisation, coordination and scheduling; those that are **centralised** and those that are **decentralised.**

There are also other issues we must consider:
- Best topology to use
- Best messaging system (IPC)
- Distributed Memory
- Clocks (as seen in topic 10)

## Recap on Shared Resources
Critical sections are enforced using a construct called a [[Topic 2 - Concurrency#Semaphores|semaphore.]] This is used to guard resources, and was initially inspired from railroads, being the original inspiration for Dijkstra's algorithm. On singular machines, shared resources must be accessed; we use critical sections via semaphores to provide this mutual exclusion.

![[Pasted image 20220328121247.png]]

## Distributed Synchronisation
For distributed systems, we have to remember that the systems are formed out of a number of machines working together.

![[Pasted image 20220328121421.png]]

There are a few considerations to be made in instances where some machines are dependent on others;
1) Is the system using synchronous or asynchronous messaging?
2) Do we block when waiting for a reply (RPC?)
3) How do we detect and recover from failures?
4) How can we enforce mutual exclusion in a distributed context?

### Distributed Mutual Exclusion
On a single machine, we can use semaphores or other shared variable to protect shared resources. With distributed systems, such methods cannot be relied upon - we need to consider a message passing system to relay this information.

There are a few things we must consider when making a distributed mutual exclusion mechanism; firstly, we must consider the application-level protocol for a critical section:

![[Pasted image 20220328122204.png]]

We also need to consider some other requirements:
1) Only one process can run in the critical section at a time.
2) Any requests to enter or exit the critical section will eventually succeed.
3) The order in which requests are received are adhered to (e.g. FIFO)

#### Central Server Algorithm
This is the simplest form of enforcing mutual exclusion, where the server acts as a central system, maintaining and coordinating access.
![[Pasted image 20220328122519.png]]

There are two other methods; ring-based, and multicast & logical clocks. We could also use *Elections.*

#### Ring-based Algorithm
This is a simple method for controlling *mutual exclusion* without the need for a central system. A token is passed clockwise around a ring of connected machines, as shown in the diagram below:
![[Pasted image 20220328122945.png]]

The algorithm itself is as follows:
1) Keep passing the token around the ring
	- When a node receives a token:
		- Check to see if the node needs access to critical section (CS)
			1) If NO -> no access is needed, so forward the token onto the next node in the ring
			2) If YES -> do the following:
				1) Keep the token (don't pass it on, as it is needed to enter the CS)
				2) Enter the Critical Section (CS)
					- Perform Instructions
				3) Once Critical Section has been finished, forward the token onto the next node in the ring.

#### Multicast and Logical Clocks
- A node would broadcast a request to all others to say it needs to access a Critical Section.
- Other nodes would have to agree to let the node start the CS.
	- However, nodes need to see if they have a request; if they do, and it has been made before the current request, they *do not agree to the new request.*
	- Clocks are used to keep track of temporal ordering of requests.

- For a node to request entering its CS, they need to:
	- Have some state information about the state of the node:
		- Released (not in/needing a CS)
		- Wanted (wants to enter a CS)
		- Held (currently in a CS)

- State changes depending on what is needed by the node:
	- If finished in a CS -> released
	- If waiting to enter a CS -> wanted
	- Entered CS -> held
		- This would only happen once it has received a message to grant access.

As for the algorithm itself:
- When a request is received:
	- If in released state, -> send message to grant access
	- If in held state: ->
		- Queue the request, but carry on with critical section (i.e. this machine has control)
		- Once CS has finished:
			- Go through the queue, send grant access message to all requests
			- Change state -> released
- If in wanted state: ->
	- Compare the *incoming request* ($node_1$) with *local node* ($node_2$)'s stored request, which was broadcast to others:
		- If the incoming request from $node_1$ is timestamped...
			- ...after the *stored request* ($node_2$); -> $node_2$ (local node) is *in the Critical Section*
			- ...before the *stored request* ($node_2$); -> send permission.

#### Coordination via Elections

Another approach to coordination can be achieved using election algorithms to satisfy mutual exclusion. This approach requires a coordinator to organise exclusion.

With an election, different nodes can *elect* a coordinator if one has not been assigned, or one stops working. Any node is suitable for the role. Any node can call an election to find a new coordinator.

A few assumptions are made:
- For an election to work, each node needs a unique identifier.
- Each node should know of the set of nodes.
- The node with the highest identifier becomes coordinator.

Examples of coordination via Elections incude the *Bully* and *Ring-based election* algorithms.

##### The Bully Algorithm

![[Pasted image 20220328124154.png]]

To determine a new coordinator (where higher ranked node bully lower ranked nodes out of the elections), we keep repeating the following process until only the highest node is left:

1) $Node_x$ will broadcast an *election* message to other nodes, where $P_{id} > Node_{P_{id}}$
	- If there is no OK message from a node with a *higher* $P_{id}$ -> broadcast the coordinator message and set the coordinator to $Node_x$.
	- If an OK message *is* received back from a node with a *higher* $P_{id}$ -> drop out of the election.

2) If a node receives an *election message:*
	- If the election message is received and the node has the *highest* $P_{id}$ -> send back a coordinator message.
	- Otherwise, -> return an OK message and start a new election.

If a node receives a coordinator message -> treat the *sender as the coordinator.*
(i.e. last node - highest $P_{id}$ - wins and becomes coordinator.)

##### Ring-based elections

This is very similar to a ring-based mutual exclusion algorithm. All nodes would be initially set to be non-participating; any node can start an election at any time - same as the *Bully* algorithm - and election/elected messages are used to coordinate things, also similarly to the *Bully* algorithm.

The algorithm would need to consider the following:
1) Initiating an election
2) Dealing with an election message
3) Dealing with an elected message (i.e. once a node has been elected).

###### Algorithm:

- Initiating an election:
	- A $Node_x$ will:
		- Change state -> to being a participant
		- Set $elected_x$ details -> to not set
		- Create an election message -> set election message id ($em_{id}$) -> $node_{id}$
		- Send an election message -> next node on ring

- Receiving an election message:
	- Compare $em_{id}$ with $node_{id}$
	- If $em_{id} > node_{id}$ ->
		- Change state -> to being a participant.
		- Set $elected_x$ details to -> not set
		- Send election message -> next node on ring.
	- If $node_{id} > em_{id}$ ->
		- Change state -> to being a participant
		- Set $elected_x$ details -> to not set
		- Update election message -> set election message id ($em_{id}$) -> $node_{id}$
		- Send election message -> next node on ring
	- If $node_{id} = em_{id}$ ->
		- Node has won the election
		- Change state -> not participating
		- Set $elected_x$ details -> $node_{id}$
		- Send elected message with $node_{id}$ -> next node on ring

- If an *elected* message is received by $Node_x$:
	- Change state -> not participating
	- Set $elected_x$ details -> $node_{id}$ from elected message
	- Check if it is the winner ->
		- YES -> election finished, all nodes should have $elected_x$ details with winning node
		- NO -> send elected message onto next node in ring.



