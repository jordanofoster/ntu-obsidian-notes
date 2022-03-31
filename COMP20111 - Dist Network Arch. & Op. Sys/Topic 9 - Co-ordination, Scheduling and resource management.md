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

## Scheduling re-cap
[[Topic 2 - Concurrency#Process Scheduling]]

To summarize:
- Multi-tasking is achieved via *processes* and *threads.*
- On a single computer, the *process manager* implements a scheduling strategy which allows dealing with many concurrent processes at the same time.
- There are three important scheduling aspects:
	- Fairness
	- Throughput
	- Response time
- There are several types of strategy:
	- First-Come, First-Served
	- Shortest Job First
	- Priority Scheduling
	- Round-robin
	- Multi-level queues
- There are problems with priority scheduling; *lottery scheduling* is a potential alternative.

### Scheduling & Load Balancing
![[Pasted image 20220328130940.png]]
When considering a distributed system, nodes need to be allocated work. There are a few things to consider:
- What is the current load of the node?
- How do you ensure an even distribution and not suffer from process starvation?
- Which type of algorithm do we use?
- How should the relevant node be chosen?
- When should nodes be contacted?

There are two types of load balancing algorithms:
- Static -> Algorithm is hard-coded using existing system knowledge
- Dynamic -> State information used to form decisions.

Getting information about network state can be done in three ways:
- Demand-driven -> Nodes disseminate information between each other. Different methods; can be sender or receiver initiated.
- Periodically driven -> Information exchanged periodically
- State-change driven -> Only when state of node changes does information get exchanged.

We still need to consider the routing of information, and the topologies used.


### Centralised approaches
- Round-Robin:
	- Centralised approach to load balancing; one of the simplest.
	- Coordinator node allocates jobs.
		- No weighting or any other metric used for allocation - just next one in sequence
- Weighted Round-Robin
	- Similar to centralised approach above.
	- This time, weighted applied for ranking of which node should be allocated a job.
	- Node at top of ranking gets job.
	- Weightings can be on anything, e.g.
		- Distance
		- Current load
		- Cores
		- Max Jobs
		- Etc.

### Scheduling Methods

There are many:
- Receiver and sender initiated
- Least connection/Least Loaded
- Min-max
- Max-min
- Opportunistic load balancing
- Equally spread current execution
- Throttled load balancing
- Ant colony optimisation
- Plus lots more!

#### Sender Initiated Algorithms
Consider the following topology of nodes:

![[Pasted image 20220328131618.png]]

In this example, overloaded (black) nodes are those where the current number of work packages in their queue exceeds a threshold value.

Underloaded (yellow) nodes are ones that can still accept new jobs, as their queues have not yet exceeded a threshold value. 

The sender initiated algorithm dictates that job migration occurs when overloaded nodes pass their threshold of queued jobs. The node will try to offload any new jobs to an underloaded node. This is a *demand-driven* method.

The overloaded node does this by polling neighbours to work out current workloads; this does however lead to the problem of additional traffic and workload, which can make a system inefficient at higher loads.

#### Receiver Initiated Algorithms
Consider the following topology:

![[Pasted image 20220328132551.png]]

Again, overloaded nodes are black and underloaded nodes are yellow. This time, the process of task migration is initiated by underloaded nodes in a demand-driven manner. For example:

- $Node_4$ is being underused because $P_{threshold} > Q_{jobs}$
- $Node_4$ will poll neighbouring nodes to see if the neighbour is overloaded (i.e. $Node_5$ will say yes)
- $Node_4$ will be given work from $Node_5$

#### Least Connection/Least Loaded
For this methods, jobs are assigned to the node with the least amount of jobs/connections. The LB will need to maintain a list of running jobs on nodes.

When received, the LB checks the list of job assignments; the node with the least current assignments is sent the job. There are several problems with this approach:
- Slower, as higher overhead needed
- Does not factor job size/duration, potentially skewing distribution
- Does not take into account node capabilities
- Can result in under utilisation of nodes (e.g., more powerful nodes do not get more workload, due to only keeping track of the least number of jobs).

#### Min-max
Also known as *Minimum-Maximum* load balancing, this is a static form of load balancing that considers the size of the job and the available resources to work out which is the best to send work to.

This is done by calculating the minimum time to complete a job in a queue of jobs; the LB goes through and ranks them from minimum length to maximum. After doing so, it distributes these jobs to nodes that can complete them in the lowest amount of time (from smallest to largest). 

This approach considers both how long the job will take, and the resources available to nodes. However it is very complex to implement, as the LB has to work out how long a job will take *without* running it. Additionally, it can cause resource starvation for larger jobs as it favours distributing smaller jobs first (which could stop longer jobs from being sent to the node).

#### Max-min
Also known as *Maximum-Minimum,* this is similar to min-maxxing, as it is also a static form of load balancing that considers job size and available resources. It differs in that it calculates the *minimum* time taken to complete all jobs in a queue, meaning that it distributes *larger jobs* first, working down to smaller jobs.

Like before, this is also complex to implement, and also causes resource starvation (but only on smaller jobs).

#### Opportunistic Load Balancing

This aims to keep nodes busy by randomly distributing jobs to nodes; it does *not* consider job size, node processing capability, or current node load. Workloads can become unbalanced due to this (as jobs are randomly assigned); for example, lower-capacity nodes could become overloaded, while higher capacity nodes are under-utilised.

#### Equally spread current execution

This aims to keep the number of running jobs on each node consistent. It does this by:
- Keeping track of which nodes are running which jobs
- When a new job is received, allocating it to the node with the least number of jobs
- Therefore, we try to ensure the evenly spread distribution of jobs by having each node run the same number of jobs.

This is easy to implement, but doesn't consider the size of a job, meaning that jobs may be balanced across nodes numerically, but workload may not. As a result, some jobs take longer to complete - causing imbalance.

This method also doesn't consider available resources (some nodes might be able to work on more jobs than others). As a result, some nodes are underutilised, resulting in a waste of money and energy.

#### Throttled load balancing

This keeps track of the load on each node in the system by storing state information for each node in a table on the load balancer. Nodes can have two states; *free* and *busy.* The method is fairly straightforward to implement:

- When a job is received -> check the table to find free nodes:
	- If nodes are found -> select one to send job to
		- Update node state from free -> busy
	- If no nodes are free -> Job is added to a queue until a node is available.
	- If a node is finished -> update node state (busy -> free)

This does, however, have disadvantages:
- It limits nodes to running one job at a time, leading to underutilisation (some can do more than one job!)
- It also does not consider job length or resource availability when selecting the job, which can result in the node becoming overloaded.

#### Ant colony optimisation

This is based on the behaviour of ant colonies:
- Ants search for food.
	- This is done by exploring the area around the "colony" in a random manor.
- When a food source is found, the ant assesses the quantity and quality of food.
- It then creates a "pheromone trail" back to the "colony".
	- Other "ants" use this trail, making it stronger (with more "pheromones") if it is a good "food source".

This technique can be applied to mapping jobs to nodes:
- In the beginning, each mapping has little information, meaning jobs are randomly assigned.
- However, as jobs are distributed, the "trails" are updated, resulting in jobs being more evenly distributed across nodes.

## Parallel Programming Issues
### Amdahl's Law
Amdahl's law states that the amount of potential speed up of a program is defined by the fraction of code that we can parallelise. The formula for potential speedup is $\frac{1}{1-P}$ where $P$ is the fraction of the code that is parallelisable.

For multi-processor systems, the formula is different; speed up is $\frac{1}{\frac{P}{N}+S}$, where:
- $P$ is the fraction of parallelised code
- $N$ is the number of nodes
- $S$ is the fraction of code that is still executed serially.

So - naturally - some types of code are more efficient on parallel/distributed systems than others.

### Optimisation Tips
When writing distributed programs, we need to consider how best to use our resources. When writing code for a single PC, we don't have to generally think about the best way to parallelise a program. To provide an example, a loop would normally be done one iteration after another (until completed).

On highly parallelised architectures, this is inefficient - one node is doing the work while the others are left unused. A loop which repeats 1000 times would be better written as the same procedure on 1000 different nodes. As a result we need to optimise code to best use parallelised resources - the *loop* construct is a good candidate for this.

#### Optimising *loops* for parallelisation
Take the following code as an example:
```
for(int i = 0; i < endValue; i++) {
	a[i] = a[i] + b[i]
}
```
When compiled, this generates code that does the following:

![[Pasted image 20220331145945.png]]

This can be done more efficiently on a parallelised system by "unpicking" the loop, to get each calculation to run on multiple machines.

With `endValue = 4`, the loop can be converted to the following:

![[Pasted image 20220331150125.png]]

This is a process known as *loop unrolling;* we are able to then send each calculation to a different compute node for processing purposes. There are a few considerations with this method; it works fine if each iteration does not rely on any previous one (i.e. there are no dependencies) and if data is available via a shared resource.

What if there *are* dependencies between each loop, though?
![[Pasted image 20220331150329.png]]

Another method that can be used is the combination of two or more loops - a process known as *loop fusion:*
```
for(int i = 0; i < 50; i++) a[i] = 0;
for(int i = 0; i < 50; i++) b[i] = 0;
```

These statements can actually be merged via the following code:
```
for(int i = 0; i < 50; i++) {
	a[i] = 0;
	b[i] = 0;
}
```

This improves the parallelism and data locality of loops, but only works if there are *no dependencies* between both loops. For example, the below pair of loops *cannot* be fused:
```
for(int i = 0; i < 50; i++) a[i] = 0;
for(int i = 0; i < 50; i++) b[i] = a[i+1] + 1; // Dependant on prior loop
```

Another method of loop optimisation is *loop tiling* - which breaks up a loop into more nests, which can then be send to different compute notes. For example;

```
int a[][] new int[10][10];
for(int x = 0; x < 10; x++) {
	for(int y = 0; y < 10; y++) a[x][y] = 1;
}
```
![[Pasted image 20220331151750.png]]

However, a problem arises: what if there are *more iterations* than there are available compute nodes?

```
int n = 10;
for(int x = 0; x < n; x += 2) {
	for(int y = 0; y < n; y += 2) {
		for(int innerX = x; inner X < Math.min(x+2, n); innerX++) {
			for(int innerY = y; innerY < Math.min(y+2, n); innerY++) {
				a[innerX][innerY] = 1; // setting to a value here but
				// complex work could be sent to compute node at this point
			}
		}
	}
}
```

The above code means that we can distribute *4* "elements" of calculation per node (instead of the assumed direct node:element mapping).

## Languages for distributed computing
There are several languages applicable for distributed computing; they provide constructs that *facilitate communication and coordination* between different system components. Some have been *designed* with distributed/parallel computing in mind.

Examples of applicable languages include Java, Julia and Go.

## Platforms for Distributed Systems:

### OpenStack
[OpenStack](https://openstack.org) provides a number of services that offer compute, storage and resources:
![[Pasted image 20220331163451.png]]

### Apache CloudStack
[Apache Cloudstack](http://cloudstack.apache.org/) is an opens-source solution that can be used to deploy both private and public *Infrastructure-as-a-Service* (IaaS) clouds amongst organisations. According to the website, it provides:
- "Works with hosts running XenServer/XCP, KVM, Hyper-V, and/or VMware ESXi with vSphere"
- Provides a friendly Web-based UI for managing the cloud
- Provides a native API
- Manages storage for instances running on the hypervisors (primary storage) as well as templates, snapshots, and ISO images (secondary storage)
- Orchestrates network services from the data link layer (L2) to some application layer (L7) services such as HCP, NAT, firewall, VPN and so on
- Accounting of network, compute and storage resources
- Multi-tenancy/account separation
- User management

### Google, Azure
There are a number of cloud-based platforms, such as [Microsoft Azure](https://azure.microsoft.com/en-us/) and [Google Cloud](https://cloud.google.com/), that offer Infrastructure or Platform-as-a-Service (I/Paas) functionality.

These platforms can also provide elastic on-demand services using a utility model on top of a virtualisation platform, and also allow the renting of virtual servers for remote login.

### Amazon Web Services (AWS)
   [AWS](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/elb-ng.pdf) is a cloud service provider that offers Cloud Computing, Storage and Load Balancing services; the lattter through Elastic Load Balancing (ELB), which can balance between 