# Corporate Architecture

## Introduction

Originally, Microsoft only provided standalone PCs - networks were sold by large vendors with thin client terminals connected to servers. *Windows for Workgroups* allowed small numbers of PC users to work together sharing files and printers. Windows NT 3/4 provided *Domains* as a concept, whereby certain servers on the network provided centralised directory services. *Active Directory* (Windows 2000) takes this further by adding layers of hierarchy to cope with larger corporate structures.

Linux machines originally could also be used alone, then in loose connectivity, then with the ue of Directory Services.

## What are Directory Services?

They are a database used to administer network resources. The following basic assumptions are made:

- Objects are relatively small
- Widely replicable and cacheable
- Mainly attributes
- Mainly reads, with occasional writes
- Frequent searching

The Internet Engineering Tasks Force solved this by standardizing the Lightweight Directory Access Protocol (LDAP) as a way to access databases over the network, but it also specifies data schema and search methods for directory services. LDAP is able to interact seamlessly with Windows Directory Services.

### Microsoft Domain vs. Workgroup

![[MSFTDomain.png]]
![[MSFTWrkGrp.png]]

Domains are an administrative boundary that acts as a primary and secondary domain controller for redundancy and duplication, and to provide load balancing. A workgroup on the other hand has no central administration, and all configurations are individually managed on each machine.

#### Microsoft Workgroup

Microsoft Workgroups are a collection of computers acting informally with no centralised authority - each computer in the workgroup has its own set of local user accounts, stored locally in a flat-file database known as the Security Accounts Manager (SAM). Passwords are stored in a hashed format; if a user needs to access another computer, they must have a valid account there as well. This can be made simpler by ensuring each user has the same account name and password on each machine, but this does cost admin time.

##### Microsoft Homegroup

With more recent versions of Windows, homegroups can be created. They allow you to share common files:
- Pictures
- Music
- Documents
- Videos
- Printers

Homegroups require a secure password to be created which allows connected devices to share and access files.

#### Microsoft Domain

For networks larger than approx. 10 computers, it is simpler to use a centralised Directory Service that contains a list of available network resources. The domain model is hierarchical, and Active Directory Domain Services (ADDS) holds the list that is trusted by all machines on the network.

For organisations, a domain provides an administrative boundary to control all physical and logical assets on a network. ADDS includes:
- Database of computers, users, etc.
- LDAP services mediate queries and responses
- Kerberos security service 
- File replication service to ensure redundancy of domain information.

##### Active Directory Data Store Physical Structure

![[ADDSPhysStruct.png]]

This is comprised of the following:

- Partitions
- Domains
- Domain trees
- Forests
- Sites
- Organisational Units

###### AD DS Partitions

The AD data store is divided up into logical partitions (also known as naming contexts):
- Domain directory
- Configuration directory
- Schema directory
- Global catalogue
- Application directory

## Domains

Domains act as an administrative boundary within the organisation and define the following:

- Replication boundaries
- Security policy boundaries
- Resource access boundaries
- Trust boundaries

### Domains and Domain Controllers

When servers are promoted to become a Domain Controller, it hosts a replica of the ADDS database. Typically domains have at least two DCs for redundancy because of how critical the information they contain is.

DCs copy information between themselves to ensure changes are propagated. This is done via multi-master replication, so that there is no need to start from a primary DC. The main issue is that the Active Directory manages this, and the consistency of information.

#### Integrating DNS & DHCP services

Microsoft encourage the integration of DNS services onto DCs, as this allows the DNS to make use of replication and/or redundancy features provided under Active Directory, provides additional security for DNS by use of group policies and avoid the need to manage DNS information separately.

When DCs do DHCP, the DHCP inherits DC permissions on DNS records, so it is advised to configure teh DHCP server with the credentials of a dedicated user account.

#### Domain Controller Issues

ADDS is important enough that DC functionality was designed to allow controlled restoration from working DCs. Faulty DCs can be brought into line with up-to-date ones by following this sequence:

1. Reboot DC under *Directory Services Restore Mode* (will need to use DSRM password supplied during original DC setting).
2. Use backup to get out-of-date DS information.
3. Restart, indicating non-authoritative restoration to acquire changes from other DCs.

Authoritative restores are requiured when deleted objects need to be forcibly restored from ADDS backup.

#### Read-Only Domain Controllers

Read-Only DCs provide mostly the same functionality as normal DCs (authentication/authorisation/DNS), but:

- Have otherwise limited functionality.
- No credentials are stored locally.
- Authentication requires access to a writable DC to authenticate requests
- Can not configure RODC with an FSMO (Flexible Single Master Operations/Operations Masters) role.

###### Why use them?

- Ideal when physical security of DC cannot be guaranteed (e.g. in an open office with no dedicated server room)
- When storing data on local storage will pose a security risk.


#### Domain Trees

![[DomainTree.png]]

Multiple domains with contiguous DNS namespaces form a domain tree. In the above example, Aardvark.com is the parent (root domain) in which child domains are created. Arrows represent two-way transitive trust between domains.

##### Forests

![[Forest.png]]

Forests are the highest level of AD DS logical structure hierarchy, and can contain one or more domain trees and one or more domain namespaces.

##### Forest Trusts

![[ForestTrust.png]]

Forest trusts provide two-way transitive trust between two connecting forest roots. In the above example, this means there is transitive trust between:

- *aardvark.com* <--> *bison.com*
- *bison.com* <--> *giraffe.com*
- But **no** default forest trust between *aardvark.com* and *giraffe.com*

Forest trusts only allow authentication to occur between forests - replication does not occur.

##### Transitive Two-way Trust

![[Trans2WayTrust.png]]

Trust allows the resources of one domain to be accessible from another (can be parent-child or tree-root trusts). By default, one-way or non-transitive trust is enabled between domains. Two-way needs to be explicitly enabled for transitive trust.

##### Shortcut Trusts

![[ShrtCutTrust.png]]

Short cut trust relationships sometimes exist in order to reduce number of hops and therefore latency. They can be one or two-way, but are not transitive; only the two domains trust each other - the others don't.

##### External Trusts

![[ExtTrusts.png]]

These are used to allow a domain external from a forest to access resources. These are not the same as a forest trust, as external trust is only between two domains (non-transitive). They are typically one-way.

##### Realm Trusts

These are used to connect a Windows Server domain to a non-Windows Kerberos realm. They can be defined as one-way, two-way, transitive or non-transitive.

![[RlmTrusts.png]]

In the above example, *us.aardvark.com* can access *tiger.com* resources using one-way, non-transitive trust, but *tiger.com* is unable to access shared resources in *us.aardvark.com*.

## Sites

The logical structure of the ADDS is independent to the physical infrastructure of the organisation's network itself. Where users and resources are located is a heavy consideration when designing an organisational structure.

Sites can be thought of as a physical area which has its own network, comprised of one or more Domain Controllers and a number of clients. There are a number of reasons for using a site when managing network traffic:

- Replication
- Authentication
- Site-aware network services

## Organisational Units

Microsoft recommends organisations to use few domains, managing administration by use of OUs, which are containers within domains and can be layered. They can also contain different types of ADDS objects:

- User
- Group
- Printers
- Organisational Units
- Computers
- Shared Folders
- Contacts
- inetOrgPerson

Objects are known by their *distinguished names* (DNs) and have attributes, both informative and administrative (e.g. for permissions). The *Schema* sets out the rules to govern what objects can be  used and how they are specified. 

Objects in containers (such as users or computers) that cannot contain other objects are called *leaf* objects. Rights and permissions are allocated to containers (and therefore the objects in them).

## Why is the architecture important?

AD involves sharing info between DCs. To let users/computers in one structure access facilities in another involves exposure of varying degrees depending on domain/tree/forest. In larger structures with many users/computers, the replication of information in the global catalogue should be minimised.

## Considerations for Internal Networking Topologies

![[NtwrkTopos.png]]

There are a variety of topologies that can be used when considering infrastructure for a corporate domain:
- Star
- Multiple Star
- Tree
- Mesh/Partial Mesh
- Wireless/Mixed

## Graphs Theory
In networking, WANs can be represent as graphs. Graphs are ways of representing relationships that exist between pairs of objects:

A graph ($G$) contains several elements:
- Vertices, $V$ (i.e. a set of objects in the graph)
- Edges, $E$ (i.e. a collection of connectors linking vertices together)

### Vertices, Adjacency and Incident
![[VertAdjIncident.png]]
Two vertices joined by an *edge* are called *end vertices/endpoints*. If the edge is directed, the first endpoint is the origin and the other the destination, e.g. E(origin -> destination) E(London -> Moscow).

Two vertices *u* and *v* are said to be adjacent if there is an edge whose endpoints are u and v, e.g.:
- London & Moscow are adjacent - i.e. E(London, Moscow)
- Rio & London are are not, as there is no such edge in this case.

An edge is considered an *incident* on a vertex if the vertex is one of the edge's endpoints, e.g.
E(New York, London) is incident to vertex V(New York) and V(London).

#### Paths
A path is a sequence of alternating vertices and edges that starts at a vertex and ends at a vertex, such that each edge is incident to its predecessor and successor vertex. For example, New York to Sydney:
	- V(New York), E(New York, London), V(London), E(London, Sydney), V(Sydney)
A path is simple if each vertex in the path is distinct. Directed paths are those in which all edges are directed.

##### Finding Paths
Routes between vertices can be found via searches, such as Breadth-first-search and Depth-first-search. These can be used to find the shortest path between two vertices, where each edge is as good as any other.

However, there are many cases, especially in network routing, where this is not appropriate. If modelling a complete network, edges could have different weightings indicating their speed (or lack thereof). BFS is the algorithm used when finding the shortest path in an undirected, unweighted graph:

```
Procedure BFS(G,v):
	q = Queue()
	q.enqueue(v)
	While q not empty:
		v = q.dequeue()
		if v not visited:
			mark v as visited //process the node
			for all edges from V to W in G.adjacentEdges(v) do:
				q.enqueue(w)
```

Algorithm for Depth-first-search:
```
Procedure DFS(G,V):
	label v as discovered
	for all edges from V to W in G.adjacentEdges(v):
		do:
			if vertex W not labeled as discovered then:
				DFS(G,w)
```

###### Weighting
![[GraphWeighting.png]]
Weighted graphs are those where a numeric label $w(e)$ is associated with each edge $e$. This is called the weight of edge $e$. Using this, the shortest (lowest latency) paths can be found.


## Hash Tables

Hash tables provide programmers with ways of storing mappings of one bit of data to another. For example, a given key would provide a value ( h("Pa\$\$word") -> 76934856434)
Hash tables can be used to associate usernames with their accounts/passwords. The hashed names would be unique and sometimes provide you with associated data.

![[HashTables.png]]

### Hash Functions

Functions need to have some way of converting a unique key to a value (e.g. $h(n)$ -> $v$). An easy way to do this is by using ASCII:

![[HashFunctionEx1.png]]

To calculate the hash value, we do: $$87 \times 31^4 + 104 \times 31^3 + 105 \times 31^2 + 116 \times 31^1 + 101 \times 31^0 = 83549193$$ $$h(White) = 83549193$$

Why use large numbers? To get an even distribution, reduce collisions and clustering.

![[HashFunctionEx2.png]]

## Compression Functions

There are two methods of compression:

1. Simple division methods using modulo arithmetic:
	- A bucket array has a known size (e.g. 1000) places
	- Position can be found by i% array length
	- h("White") = 83549193

![[CompFunctionEx1.png]]

What happens when multiple hashes point to the same point in the hash table (*Collisions*)? Either use a better compression function:

2. MAD (Multiply add and divide)
- Produces position.
- Collisions can be handled by using
	- Linear probing
	- Quadratic probing

Or implment a hash table using a bucket list/array.

### Bucket Arrays

Bucket arrays are those of size $N$. However, instead of each element storing one bit of information, elements provide another array which can grow itself:

![[BucketArrays.png]]
