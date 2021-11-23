# Sockets

## Application Programming Interface (API)

![[Pasted image 20211123003208.png]]

These are network services that provide the interface between application and protocol software, often by the operating system.

Generally, APIs provide the following functions and design features:

- A Generic Programming Interface
	- Supports multiple communication protocol suites/families.
	- Address (endpoint) representation independence
	- Provides special services for both Client and Server (sometimes?)
- Support for message oriented and connection oriented communication
- Work with existing I/O services, when this makes sense
- Operating System independence

## TCP/IP

TCP/IP itself does not include an API definition, but there are a variety of APIs for use with the stack:

- Sockets
- TLI, XTI
- Winsock
- MacTCP

### TCP/IP API Functions

The following is provided:

- Specify local and remote communication endpoints
- Initiate a connection
- Wait for incoming connection
- Send and receive data
- Terminate a connection gracefully
- Error handling

#### TCP/IP Berkeley Sockets

These are generic sockets with support for multiple protocol families, and address representation independence. They attempt to use existing I/O programming interfaces as much as possible.

##### Socket Abstraction

A socket is an abstract representation of a communication endpoint. They work with Unix I/O services, much like files, pipes and FIFOs. They obviously have special needs, such as establishing a connection and specifying communication endpoint addresses.

###### Unix file descriptor table

![[Pasted image 20211123003838.png]]

###### Unix socket descriptor table

![[Pasted image 20211123003855.png]]

##### Creating a socket

`int socket(int family,int type,int proto);`

The above code is used, where:

- `family` specifies the protocol (such as `PF_INET` for TCP/IP
- `type` specifies the type of service (`SOCK_STREAM` for TCP, `SOCK_DGRAM` for UDP)
- `protocol` specifies the protocol to use (usually `0`, meaning the default).

##### `socket()`

The `socket()` system call returns a socket descriptor, represented by a small integer, or `-1` on error. The `socket()` function itself allocates resources needed for a communication endpoint, but does not deal with endpoint addressing.

##### Specifying an endpoint address

The socket API is generic, and therefore contains a generic way to specify endpoint addresses. TCP/IP requires an IP address and port number for each endpoint address; but other protocol suites/families may use other schemes.

To understand this process, some background information is required:

###### POSIX data types

The Portable Operating System Interface (POSIX) is a family of standards specified by the IEEE Computer Society, for maintaining compatibility between operating systems.

![[Pasted image 20211123004614.png]]
![[Pasted image 20211123004624.png]]

##### Generic socket addresses

```
struct sockaddr {
	
	uint8_t			sa_len; /* sa_len used by kernel */
	
	sa_family_t 	sa_family;
	
	char			sa_data[14];

};
```

`sa_family` specifies the address type, whereas `sa_data` specifies the address value.

##### `sockaddr`

In this example, we use addresses that will allow a man to use sockets to communicate with his family, using address type `AF_FAMILY` and the following address values:

- Daughter - `1`
- Wife - `2`
- Mom - `3`
- Dad - `4`
- Sister - `5`
- Brother - `6`

###### `AF`