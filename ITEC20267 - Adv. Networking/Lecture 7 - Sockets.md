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

- Specfication of local and re

