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

#### Socket Abstraction

A socket is an abstract representation of a communication endpoint. They work with Unix I/O services, much like files, pipes and FIFOs. They obviously have special needs, such as establishing a connection and specifying communication endpoint addresses.

##### Unix file descriptor table

![[Pasted image 20211123003838.png]]

##### Unix socket descriptor table

![[Pasted image 20211123003855.png]]

#### Creating a socket

`int socket(int family,int type,int proto);`

The above code is used, where:

- `family` specifies the protocol (such as `AF_INET` for TCP/IP
- `type` specifies the type of service (`SOCK_STREAM` for TCP, `SOCK_DGRAM` for UDP)
- `protocol` specifies the protocol to use (usually `0`, meaning the default).

#### `socket()`

The `socket()` system call returns a socket descriptor, represented by a small integer, or `-1` on error. The `socket()` function itself allocates resources needed for a communication endpoint, but does not deal with endpoint addressing.

#### Specifying an endpoint address

The socket API is generic, and therefore contains a generic way to specify endpoint addresses. TCP/IP requires an IP address and port number for each endpoint address; but other protocol suites/families may use other schemes.

To understand this process, some background information is required:

##### POSIX data types

The Portable Operating System Interface (POSIX) is a family of standards specified by the IEEE Computer Society, for maintaining compatibility between operating systems.

![[Pasted image 20211123004614.png]]
![[Pasted image 20211123004624.png]]

#### Generic socket addresses

```
struct sockaddr {
	
	uint8_t			sa_len; /* sa_len used by kernel */
	
	sa_family_t 	sa_family;
	
	char			sa_data[14];

};
```

`sa_family` specifies the address type, whereas `sa_data` specifies the address value.

#### `sockaddr`

In this example, we use addresses that will allow a man to use sockets to communicate with his family, using address type `AF_FAMILY` and the following address values:

- Daughter - `1`
- Wife - `2`
- Mom - `3`
- Dad - `4`
- Sister - `5`
- Brother - `6`

#### `AF_FAMILY`

By initializing a `sockaddr` structure to point to the *Daughter* address, we use the following code:

```
struct sockaddr mary;

mary.sa_family = AF_FAMILY;
mary.sa_data[0] = 1;
```

#### `AF_INET`

For the `AF_FAMILY` protocol, only 1 byte was needed to specify the address. For `AF_INET`(TCP/IP), we need the following; a 16-bit port number, and, exclusively for IPv4, a 32-bit IP address.

##### `struct sockaddr_in`  (IPv4)

![[Pasted image 20211123005521.png]]

##### `struct sockaddr_in` (IPv6)

![[Pasted image 20211123005600.png]]

#### Network Byte Order

All values stored in a `sockaddr_in` struct must be in *network byte order.* For example:

- `sin_port` is a TCP/IP port number.
- `sin_addr` is an IP address.

This is a common mistake!

##### Network Byte Order Functions

Where the following applies:

- `h`: host byte order
- `n`: network byte order
- `s`: short (16-bit)
- `l`: long (32-bit)

```
uint16_t htons(uint16_t); /* Host Byte Order to Network Byte Order (Short) */
uint16_t ntohs(uint1_16_t); /* Network Byte Order to Host Byte Order (Short) */
uint32_t htonl(uint32_t); /* Host Byte Order to Network Byte Order (Long) */
uint32_t ntohl(uint32_t); /* Network Byte Order to Host Byte Order (Long) */
```

#### TCP/IP Addresses

In this instance, we don't need to deal with `sockaddr` structures, since we will only deal with a real protocol family - instead, we can use `sockaddr_in`.

However, there is a caveat - the C functions that make up the sockets API expects `sockaddr` structures, not `sockaddr_in`.

##### TCP/IP Address Structures

![[Pasted image 20211123010556.png]]

##### TCP/IP - `bind()`

The `bind()` syscall is used to assign an address to an existing socket, as seen below:

```
int bind(int sockfd, const struct sockaddr *myaddr, int addrlen)
```
Note the `const struct` here.

`bind()` returns 0 on success, and -1 on error. Calling `bind()` assigns the address specified by the `sockaddr` structure to the socket descriptor. You can give `bind()` a `sockaddr_in` structure as well:

```
bind(mysock, (struct sockaddr*) &myaddr, sizeof(myaddr) );
```

###### Example of `bind()`

```
int mysock,err;

struct sockaddr_in myaddr;

mysock = socket(PF_INET,SOCK_STREAM,0);

myaddr.sin_family = AF_INET;

myaddr.sin_port = htons(portnum);

myaddr.sin_addr = htonl(ipaddress);

err=bind(mysock, (sockaddr *) &myaddr, sizeof(myaddr));
```

###### Use cases for `bind()`

There are a number of them:
- The server would like to bind to a well known address (port number).
- Client can bind to a specific port.
- The client can ask the OS to assign *any* available port number.

Clients don't typically care about what port they are given. When `bind()` is used, however, it can be told to assign you any available port, as seen below:

`myaddr.port = htonx(0);`

##### TCP/IP - Address Assignment

There is no realistic way to know the right IP address to give to `bind()` - the IP address should instead be specified as `INADDR_ANY`, as this tells the OS to take care of this problem on our behalf.

###### TCP/IP - Address Conversions

The following code converts ASCII dotted-decimal IP addresses to a network-byte-ordered 32-bit value, returning `1` on a success, and `0` on a failure;

`int inet_aton(char *, struct in_addr *);`

This line, on the other hand, does the reverse - changing a network-byte-ordered value to an ASCII dotted-decimal (or string-format IP address):

`char *inet_nota(struct in_addr);`


Using `family`, `string_ptr` and `address_ptr`, this line converts the IP address string to a network-byte-ordered 32 or 128-bit value, returning 1 on success, -1 on failure, and 0 on invalid input:

`int inet_pton(int, const char *, void *);`

Using `family`, `address_ptr`, `string_ptr` and `length`, this converts a network-byte-ordered value to an IP address string, in the format `x:x:x:x:x:x:x:x` or `x:x:x:x:x:x:a.b.c.d`:

`char *inet_ntop(int, const void*, char*, size_t);`

##### TCP/IP - Other Socket System Calls

![[Pasted image 20211123012142.png]]

##### Example TCP/IP Python Scripts

###### Client

```
import socket
import sys
import timeit

def get_constants(prefix):
	"""Create a dictionary mapping socket module constants to their names."""
	return dict( (getattr(socket, n), n)
		for n in dir(socket):
			if n.startswith(prefix):
		)

families = get_constants('AF_')
types = get_constants('SOCK_')
protocols = get_constants('IPPROTO_')

# Create a TCP/IP socket
sock = socket.create_connection(( '192.168.1.201', 10000))

print( 'Family :', families[sock.family], file=sys.stderr)
print( 'Type :', types[sock.type], file=sys.stderr)
print( 'Protocol:', protocols[sock.proto], file=sys.stderr)
print(file=sys.stderr)

try:
	
	# Send data
	message = 'This is the message. It will be repeated.'
	for i in range(20):
		message += 'This is the message. It will be repeated.'
	print ('sending "$s"' % message, file=sys.stderr)
	start = timeit.timeit()
	while True:
		sock.send(message.encode())
		end = timeit.timeit()
		if (end - start) > 25:
			break
		
	amount_received = 0
	amount_expected = len(message)
	
	while amount_received < amount_expected:
		data = sock.recv(100).decode()
		amount_received += len(data)
		print('recieved "%S"' % data, file=sys.stderr)
except:
	print('Ooops, error occured', file=sys.stderr)
finally:
	print('closing socket', file=sys.stderr)
	sock.close()
```

###### Server

```
import socket
import sys
import timeit

# Create a TCP/IP socket
sock = socket.socket(socket.AF_INET, socekt.SOCK_STREAM)

# Bind the socket to the port
server_address = ('localhost', 10000)
print('starting up on %s port %s' % server_address, file=sys.stderr)
sock.bind(server_address)

# Listen for incoming connections
sock.listen(1)

while True:
	# Wait for a connection
	print('waiting for a connection', file=sys.stderr)
	connection, client_address = sock.accept()

try:
	print('connection from', client_address, file=sys.stderr)
	
	# Receive the data in small chunks and retransmit it
	start = timeit.default_timer()
	dsize = 0;
	while True:
		data = connection.recv(3000000).decode()
		dsize += len(data)
		end = timeit.default_timer()
	# 		print('current data size= ', dsize, end - start, file=sys.stderr)
		if (end - start) > 20:
			print('data size for 20 sec =', dsize, file=sys.stderr)
			break
	#	print('received "%s"' % data, file=sys.stderr)
		if data:
			dummy = 0
			print('sending data back to the client', file=sys.stderr)
			connection.sendall(data.encode())
		else:
			print('no more data from', client_address, file=sys.stderr)
			break
			
	