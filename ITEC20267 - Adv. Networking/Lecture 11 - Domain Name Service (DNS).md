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

In the 1970s, ARPANET mainly used a hosts.txt file maintained by the SRI-NIC. It was pulled from a single machine, and 