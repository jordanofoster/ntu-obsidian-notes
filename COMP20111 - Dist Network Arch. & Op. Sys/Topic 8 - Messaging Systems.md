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

A User Datagram Packet is a connectionless form of transmission. i.e.


