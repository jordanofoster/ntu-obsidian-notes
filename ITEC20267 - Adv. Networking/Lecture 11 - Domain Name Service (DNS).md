# Domain Name Service (DNS)

This lecture covers the following aspects of DNS architecture, including:
- Resolvers
- Caching forwarders
- Authoritative servers
- Timing parameters

## Purpose of Domain Names

Addresses are used to locate objects, but names are easier for humans to remember than numbers. As a result, we want to be able to link domain names to IP addresses (as the latter is easier for machines to read). The domain name service provides a mapping from domain names to resources of several different types.

### Names and Addresses in General

Addresses are typically how we get to an endpoint, and are typically hierarchical (for scaling purposes):

| Object | Addresses|
| --- | --- |
| Nottingham Trent University | `152.71.143.11`, +446503816003 |

Names are how an endpoint is referenced. There us typically no structurally significant hierarchy. Examples include names ("David"), Locations ("Tokyo"), and, of course, domain names ("itu.int").

#### History of Naming

In the 1970s, ARPANET mainly used a hosts.txt file maintained by the SRI-NIC. It was pulled from a single machine, and was essentially a list of what IP addresses resolved to which hostnames. This caused many problems, including but not limited to traffic/load issues, name collisions and consistency.

DNS was created in 1983 by Paul Mockapetris as a response to these issues, being published under RFC 1034/1035, and later modified updated and enchanced by subsequent RFCs.

## DNS

DNS is a lookup mechanism for translating objects into other objects. It acts as a globally distributed, loosely coherent, scalable and reliable dynamic database. It contains three components; a namespace, servers that host the namespace, and resolvers (clients) that query these servers about the namespace.

### Features

#### Global Distribution

Data is maintained locally, but retrievable globally. No single computer has all DNS data. Lookups can also be performed by any device, and remote DNS data is locally cachable to improve performance.

#### Loose Coherency

DNS databases are always internally consistent; each version of a subset of the database (a zone) has a serial number that increments on each database change. Changes to the master copy of the database are replicated according to timing set by the zone administrator. Cached data also expires according to a set timeout.

#### Scalability

There is no limit to a size of a DNS server. For example, one server has over 20,000,000 names (although this is not a good idea). There is also no limit to the number of queries; 24,000 queries per second can be easily handled. Queries are distributed amongst masters, slaves and caches.

#### Reliability

Data is replicated, as it is copied from the master to multiple slaves. Clients can query the master server and any of the copies at slave servers, though they will typically prefer to query local caches.

DNS as a protocol can also use either UDP or TCP; if the former, the protocol automatically handles issues such as retransmission, sequencing, etc.

#### Dynamicity

The database can be updated dynamically, meaning that any record can be added, deleted or otherwise modified. Modification of the master database triggers replication, as it is the only one that can be dynamically updated. As a result, it ends up becoming a single point of failure.

## DNS Concepts

### DNS Names

A DNS namespace needs to be hierarchical in order to scale. Objects are named based on the following:
- Location
	- Within country
	- Set of organizations
	- Set of companies, etc.
- Unit within that location
	- Company within set of company, etc.
- Object within a unit
	- Name of a person within the company

#### Fully Qualified Domain Names (FQDNs)

An example of this is `WWW.RIPE.NET.` - notice the ***trailing dot.*** 

DNS provides mapping from an initial FQDN to resources of several types, and names are used as a key when fetching data within the DNS.

##### DNS Resource Records (RR)

The DNS maps names into data through the use of Resource Records, as shown below:
![[Pasted image 20220124134724.png]]

#### DNS Names Concept

Domain names can be mapped to a tree; new branches are made at the 'dots', and there is no restriction to the amount of branches.

![[Pasted image 20220124135043.png]]

#### DNS

Domains themselves are considered namespacs. For example, everything below the top-level domain .com is in the `com` domain, and everything below ripe.net is in the `ripe.net` domain and in the `net` domain.

![[Pasted image 20220124141542.png]]

##### DNS Delegation

Administrators can create subdomains to group hosts, according to one or more of geography, organizational affliation or any other criterion. Admins of the domains themselves can also delegate responsibility for managing a subdomain to someone else (although this isn't required).

A parent domain retains links to its delegated subdomains, by "remembering" who the subdomain was delegated to.

###### Zones and Delegations

Zones are administrative spaces, where the admins are responsible for a portion of a domain's namespace. Authority is delegated from a parent, and to a child.

![[Pasted image 20220124141853.png]]

#### Nameservers

Nameservers answer DNS questions; there are several types:
- Authoritative servers
	- Master (primary)
	- Slave (secondary)
- Recursive (caching) server
	- Alongside caching forwarders
- Nameservers that mix functionality.

##### Authoritative Nameservers

These give authoritative answers for one or more zones; the master server normally loads the data from a zone file, whereas a slave server normally replicates the data from the master server via a zone transfer.

![[Pasted image 20220124142120.png]]

##### Recursive Servers

Recursive servers typically do the actual lookups, as they ask questions to the DNS on behalf of the clients. The answers they provide are obtained from authoritative servers, but the actual answers forwarded to the client are not marked as such.

Previous answers are stored for future reference in the server's cache.

##### Resolvers

Resolvers ask questions to a DNS system on behalf of the application. This is normally implemented via a system library such as libc, as shown below:
```
gethostbyname(char *name);
gethostbyaddr(char *addr, int len, type);
```

###### Resolving Process & Cache

Using question `www.ripe.net A` (what is the A record of domain www.ripe.net?):

![[Pasted image 20220124142616.png]]

#### Resource Records (more detail)

Reource records consist of their names, TTL, class, type and RDATA:
- TTL is a timing parameter.
- the IN class is the widest used.
- There are multiple types of RR records
- Everything behind the type identifier is under RDATA.

![[Pasted image 20220124142809.png]]

###### Examples of DNS RRs in a zone file

![[Pasted image 20220124142857.png]]

###### DNS RRs: SOA and NS (Nameserver) records

The SOA and NS records are used to provide information about the DNS server itself. The NS indicates where information about a given zone can be found:

```
ripe.net. 7200 IN NS ns.ripe.net
ripe.net. 7200 IN NS ns.eu.net
```

The SOA record provides information about the start of authority (i.e. the top of the zone), also known as the APEX:





