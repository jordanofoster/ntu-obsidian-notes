# Messaging Systems

## Single vs Multiple Systems

When writing an application, it tends to be written as a single program running on a single computer. However, this approach does not work when a program is scaled to run over multiple systems. 7

As such, we need to consider how the problem can be solved by distributing functionality across multiple programs, running on multiple nodes.  We also have to consider how to access this functionality remotely, in the form of a method or object. There are a number of approaches, and they are mainly categorised as direct or indirect:

![[Pasted image 20220221131317.png]]
![[Pasted image 20220221131321.png]]
![[Pasted image 20220221131329.png]]

## Local Procedure Calls

Java programs require methods to be written to call other methods. This procedure is called *local procedrure calling*. An example of such is shown below:

```
Receiver receive = new Receiver(destinationPort);
Sender send = new Sender(3000, destinationPort);

receive.start();
send.start();
```
![[Pasted image 20220221131626.png]]
The question however, is what, in fact, is happening, and what must be done if the method that we want to call is stored on a remote machine:

### Remote Procedure Calls (RPCs)

![[Pasted image 20220221131816.png]]

There are several things we must consider with RPCs:
1) How do we pass information?
2) How do we return information?
3) How are errors handled?

## Network Programming using Java

Java provides access to a comprehensive set of packages and classes for accessing and transmitting/receiving information across a network. To include networking functionality, `java.net.*` must be imported. This package provides access to a number of classes:
- `InetAddress`
- `DatagramPacket`
- `DatagramSocket`
- `Socket`
- `SocketServer`

### UDP Programming under java

A User Datagram Packet is a connectionless form of transmission (i.e. the packet will be routed via a packet-switched network). To create a packet, the following line is required:

`packet = new DatagramPacket(buffer.length, addr, destinationPort)`

`buffer` is the space you want to store when receiving or sending the information. This needs to be definined as `Bytes[]`, but `string.getBytes()` could be used instead (***when sending***).
![[Pasted image 20220221132556.png]]

- `buffer.length` represents how many bytes of information to send.
- `addr` refers to the address of the destination machine.
- `destinationPort` refers to the port of the destination machine.
![[Pasted image 20220221132627.png]]

Once `DatagramPacket` has been created, a `DatagramSocket` object is needed to send it.

![[Pasted image 20220221132645.png]]

To create a socket on the sending machine, a port to transmit it on is required:
```
DatagramSocket socket = new DatagramSocket(3000); // DatagramSocket(<socket>)
socket.send(packet); // DatagramPacket
socket.close();
```

`DatagramSocket` has two important methods:
- `send(<packet>)`
- `recieve(<packet>)`

Another example of code shown below:
```
DatagramSocket socket = new DatagramSocket(4000);
socket.setSoTimeout(0);
byte []buffer = new byte[1024];
DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
socket.receive(packet);
String message = new String(buffer);
System.out.println("Got message: " + message.trim());
socket.close();
```

## Socket & Multi-threaded Programming using Java

For Client/Server systems, a `ServerSocket` can be used to accept multiple connections from clients:

```
ServerSocket serverSocket = new ServerSocket(listeningPort, connectionQueueSize);
while (true) {
	Socket clientSocket = serverSocket.accept();
	// ....
}
```

When dealing with multiple connections, we would need to use a multi-threaded approach to designing and writing our applications.

### Socket Communication: Single Client to Server

![[Pasted image 20220221133500.png]]

### Multi Client to server
![[Pasted image 20220221133534.png]]

## Server systems using messages
![[Pasted image 20220221133736.png]]

Another key approach to distributed and server programming is through the receiving and sending of messages (i.e. a messaging system). There are a few factors to consider:
1) The messages and their structure
2) How are messages sent?
	- Directly?
	- Broadcast?
	- Multicast?
3) How are messages sequenced?
4) How to write servers to receive and process messages

Additionally, it still needs to be multi-threaded; one thread for receiving and one for sending.

## Types of communication

Some of the issues when programming systems have already been looked at prior, although more will be covered in this topic and subsequent topics:

- Messaging systems are used to enable communication between two or more 'devices' in a distributed system.
- RPC and programming methods that we have looked at so far are classed as *direct coupling* between a sender and receiver.
	- They are susceptible to points of failure (at the client and/or server), and are not easily adaptable to change.
- For messaging systems to be used, they need to be flexible and able to adapt to change.
- These types of *indirect* systems exhibit:
	- Space uncoupling
	- Time uncoupling
	- Flow uncoupling

Messaging systems themselves can be broadly categorised into the following:
- Group communication
- Publish/Subscribe
- Message Queues
- Distributed shared memory

### Group Communication

Group based communication builds upon *multicast* communication. Systems can join or leave a group of systems; the implication being that systems will be part of a group membership.

A service is used to recieve and deliver messages to all group members. Group communication itself requires the following:

- *Reliable communication* to large numbers of group members
	- *Integrity*, to ensure that the message received is the same as is sent.
	- *Valdity*, to ensure that messages will eventually be delivered
	- *Agreement*, to ensure that where messages are delivered to one system, all others systems in the group also receive the message.
- Maintenance of *message order* (i.e. if a message occurs before another message in a distributed system, the ordering is maintained).
- Group membership management
- Failure detection

A small example group communication system is located in [week 18's activities](https://now.ntu.ac.uk/d2l/le/content/803352/viewContent/5818764/View)

### Publish/Subscribe

Publish/Subscribe is another form of messaging system used in Distributed Systems. They are formed out of a set of producers (publishers) and a set of consumers (subscribers). An example of a producer/consumer set is shown below:

![[Pasted image 20220221140320.png]]

Examples include embedded system processing events, and the FIFO buffer storing data.

Publish/Subscribe systems are formed out of a set of *producers* (publishers) and a set of *consumers* (subscribers).

Publishers generate events and subscribers are notified when something interesting happens:

![[Pasted image 20220221140944.png]]
![[Pasted image 20220221141003.png]]
![[Pasted image 20220221141011.png]]

### Message Queues

When looking at Publish/Subscribe systems, the concept of producers/consumers was revisited, as mentioned in [[Topic 2 - Concurrency#The Producer-Consumer Problem|Topic 2.]] Distributed message queues are very similar to how producers/consumers work:

1) Producers *send* information to the queue
2) Consumers can extract information from the queue in three ways:
	1) *blocking receive* - block until the message is available
	2) *non-blocking receive* - polls to see if the message is available
	3) *notify* - gets notified that the message is available (similar to Publish/Subscribe)

![[Pasted image 20220221141326.png]]

### Distributed Memory

