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
- ``