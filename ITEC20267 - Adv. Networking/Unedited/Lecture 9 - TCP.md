# TCP
## Transport Layer
The transport layer provides *logical communication* between application-layer processes running on different hosts. Transportation protocols themselves run on end systems as two sides:

- On the sending side, the protocol breaks application messages into *segments* and passes them onto the network layer.
- On the receiving side, segments are reassembled into messages and passed back to the application layer.

More than one transportation layer protocol is available to applications, with the main two being TCP and UDP.

A good way to think of things is that the *network layer* provides *logical comunication* between *hosts,* whereas the *transport layer* builds upon this by allowing logical communication *between processes* on each host. An analogy involving a household is shown below:

![[Pasted image 20220111233128.png]]

## UDP
UDP is a very barebones Internet transport protocol that attempts to be a best effort service; UDP segments may be lost or delivered out-of-order to the application. The protocol is *connectionless*, meaning that no handshaking occurs between the sender and receiver, and each UDP segment is treated independently of others (i.e. there is no packet numbering).

UDP is typically used for applications where bandwidth is limited, be it by the amount of data transferred or the lack of quality in the connection itself. This includes things such as streaming/multimedia apps (which can compensate for packet loss - but not for low data rates), and network-discovery protocols such as DNS and SNMP. The protocol itself lacks any reliability measures, and as such they must be implemented at the application layer (such as error recovery).

### UDP Segment Format
![[Pasted image 20220111215300.png]]
In this instance, `length` refers to the length of the UDP segment as a whole in bytes (including the header).

#### Why does UDP exist?
Several aspects of UDP's sister protocol, TCP, add delay to network communications, including:
	- Connection establishment
	- Tracking connection state
	
UDP naturally does not face these issues. In addition, the protocol's small header size reduces overhead further, and the lack of congestion control means that UDP's only limits on data-rate are those imposed by the layers below it. This makes it naturally suitable for situations where data needs to reach another system quickly, but not completely.

A good way to think about this is to consider telephony, which itself uses UDP - if voice data comes through at a low quality (as opposed to simply cutting out), a user on the other side will be able to subconsciously use hueristics to determine what was said with a reasonable amount of accuracy. This concept of 'close enough' can be adapted to fit many modern usecases for the protocol.

## TCP Services

TCP as a protocol provides the following services:
- Connection Orientation - applications must request a connection *to* a destination and then use it to transfer data.
- Point-to-Point communication - as each TCP connection has *two* endpoints.
- Complete reliability - TCP guarantees that data sent is delivered uncorrupted and in order.
- Full Duplex Communication - data flows in either direction and may be sent at any time.
	- TCP can buffer outgoing and incoming data in both directions.
- Stream Interface - data is sent as an uninterpreted continuous sequence of octets along the connection. TCP does not keep records, and there is no guarantee that data is received in the same packet length as it is sent.
- Reliable Connection Startup - TCP requires that 2 applications must agree to a connection being formed before it is actually created.
	- Duplicate packets used in previous connections are not valid responses, nor will they otherwise interfere with the new connection.
- Graceful Connection Shutdown - An application program can open a connection, send arbritrary amounts of data, and then request that it be shut down. TCP guarantees that all data is delivered reliably before a connection can be closed.

### End-to-End TCP Service

![[Pasted image 20220111221951.png]]

TCP provides connections directly from an application on one computer to an application on a remote computer; these are virtual, as they are achieved in software. The TCP protocol itself uses the IP stack to carry messages.

#### Packet Loss and Retransmission

![[Pasted image 20220111222019.png]]

##### Adaptive Retransmission
TCP estimates the *round-trip* delay for each active connection by measuring the time needed for a response to be received. The protocol also records the time that a message was sent.

When the response arrives, a new estimate for the round-trip delay is calculated, via a statistical function that produces a weighted average and variance, and uses a linear combination of the estimated mean and variance as a value for retransmission.

###### Calculation for Retransmission Time
The equation is as follows:

$EstimatedRT = (1 - \alpha) \times EstimatedRTT + \alpha \times SampleRTT$

This represents an exponential *weighted* moving average. The influence of the past sample therefore decreases exponentially fast; typically, $a = 0.125$.

![[Pasted image 20220111222542.png]]

###### Comparison of Retransmission Times
![[Pasted image 20220111231413.png]]

## Buffers, Flow Controls and TCP Windows
![[Pasted image 20220111231430.png]]

## TCP Three-Way Handshakes
![[Pasted image 20220111231504.png]]
Three-way handshakes are used to close a connection; ACKs are sent in each direction to guarantee that all data has arrived before the connection is closed.


## TCP Segment Header Format
![[Pasted image 20220111231611.png]]

TCP uses a single format for all messages; TCP connections themselves contains 2 streams of data. The *acknowledgement number* and *window* header values refer to incoming data, whereas the *sequence number* header value refers to outgoing data.

### Principles of reliable data transfer

This is important at the application, transport and link layers of the TCP/IP stack.
![[Pasted image 20220111231748.png]]
The characteristics of an unreliable channel will determine the complexity of the reliable data transfer protocol (`rdt`).

#### Pipelined Protocols

Pipelining refers to when the sender allows multiple packets to be sent without acknowledgement after each transmission. This involves a range of sequence numbers being increased, and buffering on the sender and/or receiver's end. 
![[Pasted image 20220111232120.png]]
There are two generic forms of pipelining protocols; *go-back-N* and *selective repeat*.

#### Example of pipelining increasing efficiency
![[Pasted image 20220111232243.png]]

#### Pipelining Acknowledgement Schemes

##### Go-back-N

With this, the sender can have up to $N$ unacknowleged packets in the pipeline; the receiver only sends a *cumulative acknowledgement* for these, instead of an acknowledgement per-packet. If there is a gap in the pipeline, the cumulative acknowledgement is split into two for every unreceived stream of packets.

The sender keeps a timer for the oldest unacknowleged packet; when expired, *all* unacknowledged packets are retransmitted.

##### Selective Repeat

The sender can have up to $N$ unacknowledged packets in the pipeline. The receiver will send an *individual* acknowledgement for each packet. The sender maintains an individual timer for each unacknowleged packet; when this expires, *that specific packet* is retransmitted.

## Summarized Notes:

- Transport layer protocols provide a form of *logical communication* between application processes running on different hosts. [[Lecture 9 - TCP#Transport Layer|(1)]]
- TCP provides reliable, ordered delivery of packets. It does this using the following [[Lecture 9 - TCP#TCP Services|(2)]]:
	- Congestion control
	- Flow control
	- Mandatory connection setup 
- UDP is unreliable and unordered, but acts as a low-overhead extension of the IP stack for high-bitrate purposes. [[Lecture 9 - TCP#UDP|(3)]]
- TCP is a *connection-oriented* protocol; UDP is *connectionless.*

- For the *Go-back-N* acknowledgement scheme [[Lecture 9 - TCP#Go-back-N|(4)]]:
	- The sender can have up to $N$ unacknowledged packets in the pipeline.
	- The receiver only sends *cumulative acknowledgements.*
- For the *Selective Repeat* acknowledgement scheme [[Lecture 9 - TCP#Selective Repeat|(5)]]:
	- The sender can have up to $N$ unacknowledged packets in the pipeline.
	- The receiver sends *individual acknowledgements* for each packet.