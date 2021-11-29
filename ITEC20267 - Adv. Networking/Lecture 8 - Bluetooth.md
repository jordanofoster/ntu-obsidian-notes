# Bluetooth

## Bluetooth Basics

Bluetooth was created by a consortium of various companies, including Ericsson, Intel, IBM, Nokia and Toshiba, amongst others. Bluetooth as a protocol aims to cover several scenarios, including:

![[Pasted image 20211129164111.png]]

- Connection of peripheral devices, such as loudspeakers, joysticks and headsets
- Support of ad-hoc networking using low-cost, small devices
- Bridging of networks, such as GSM (via phone) → Bluetooth → Laptop

Bluetooth also acts as a simple, cheap replacement of IrDA, as it is low-range, low data-rate and low power. It operates over the 2.4Ghz band worldwide, and has various design considerations to serve this purpose, including but not limited to:

- Resistance to jamming and selective frequency fading
	- Supported via FHSS over 79 channels of 1MHz each, and supporting 1600 hops/second
- Coexistence of multiple piconets, like CDMA
- Via both synchronous connections (SCO) and asynchronous, connectionless methods, links are supported
- Interoperability, as the protocol stack supports TCP/IP, OBEX and SDP
- Range of 10 meters, extendible to 100

The <a href = "https://www.bluetooth.com">documentation</a> itself is over 1000 pages long.

### Bluetooth Application Areas

Bluetooth can be applied in the following areas:

- Data and voice access points
	- Real-time voice and data transmissions
- Cable replacement
	- Bluetooth removes the need for numerous cable attachments for communication
- Low implementation cost networking, < $5
- Ad hoc networks
	- Devices with a Bluetooth radio can establish a connection with another device when in range

### Bluetooth Protocol Architecture

Bluetooth is a layered protocol architecture - this means it is built upon various other protocol stacks, which deal with different roles; including core protocols, cable replacement/telephony control protocols and adopted protocols (through implementation of the prior).

![[Pasted image 20211129162035.png]]

The above diagram represents the entire network stack of the Bluetooth protocol; it is broken down as such:

- At the lowest-level, the radio used for Bluetooth runs in the 2.4Ghz frequency band, as stated prior.
	- This is modulated using Gaussian [[Lecture 3 - Modulation Techniques#Frequency-shift Keying FSK|FSK]].
- The baseband itself uses *Frequency-hopping spread spectrum* (**FHSS**), a method supported by 79 carriers - it also makes use of CDMA, which defines a hopping sequence using the MAC addresses of nodes.
- Audio interfaces directly with the baseband layer, with each voice connection being over a 64Kbps SCO link - the encoding scheme used for this is <a href=https://en.wikipedia.org/wiki/Continuously_variable_slope_delta_modulation>Continuous Variable Slope Delta (CVSD)</a> modulation.
- The *Link Manager Protocol* (**LMP**) defines link setup and control methods, alongside authentication and encryption procedures.
- The *Host Controller Interface* (**HCI**) provides a uniform access method to the baseband, control registers and other low-level components via physical interfaces, such as USB, PCI or UART.
- The *Logical Link Control and Adaptation Layer* (**L2CAP**) contains higher-level protocols that assist with multiplexing, packet segmentation/reassembly and <a href=https://www.fortinet.com/resources/cyberglossary/qos-quality-of-service>Quality of Service (QoS).</a>
- The Service Discover Protocol (SDP) assists in locating services provided by another Bluetooth device.
- The Telephony Control Specification (TCS) defines the call control signalling, for establishing speech/data calls between Bluetooth devices.
- RFCOMM provides emulation of serial links (typical over physical interface RS232). Up to 60 connections are supported.

#### Core Protocols

This includes the following:
- Radio
- Baseband
- Link Manager Protocol (LMP)
- Logical link control and adaptation protocol (L2CAP)
- Service discovery protocol (SDP)

#### Cable Replacement Protocol

RFCOMM is used as a form of cable replacement protocol

#### Telephony Control Protocol

The Binary Telephony Control Specification (TCS BIN) is used here.

#### Adopted Protocols

These are protocols Bluetooth inherently implements as part of being a layered architecture:

- PPP (Point-to-Point Protocol)
- TCP/UDP/IP
- OBEX (Object Exchange)
- WAE/WAP (Wireless Application Environment/Wireless Application Protocol)

### Bluetooth Usage Models

There are **6** usage models for Bluetooth; they are listed below:

- File transfer
- Internet bridge
- LAN access
- Synchronization
- Three-in-one phone
- Headsets

### Bluetooth Terminology

*Piconets* are basic units of Bluetooth networking, containing one *Master* and one-to-seven *Slave* devices. The *Master* device determines the channel and phase of the ad-hoc network.

*Scatternets* are an accumulation of piconets; a device in one piconet may exist as a master or slave in another piconet. Scatternets allow many devices to share the same area, and make efficient use of bandwidth.

#### Bluetooth Networks

An example of various wireless Bluetooth network topologies is shown below:

![[Pasted image 20211129163656.png]]

##### Bluetooth Network Topologies

![[Pasted image 20211129163828.png]]

Piconets, as stated before, are a set of Bluetooth nodes (*Slaves*) synchronized to a master node. The piconet hopping sequence is derived from the Master device's MAC address, and is defined as `BD_ADDR`, an IEEE802 48-bit compatible address.

*Master* and *Slave* devices can switch roles, but nodes can only be masters of *one* piconet. `Q: Why?`

###### Bluetooth Scatternets

![[Pasted image 20211129174021.png]]

Within each piconet, the master determines the hopping sequence of the network, and slave devices must synchronize to this, as it is the literal definition of participation within the piconet. Communication between several piconets involves devices jumping back and forth between each of them.

### Bluetooth Radio Specification

There are three classes of transmitters within the spec:

- **Class 1** - outputs 100mW for maximum range.
	- Power control is mandatory, and this provides the greatest distance.
- **Class 2** - outputs 2.4mW at maximum.
	- Power control is optional for this class.
- **Class 3** has a nominal output of 1mW, and is the lowest power class.

#### Frequency Hopping in Bluetooth

This provides resistance to interference and multipath effects, alongside a form of multiple access among co-located devices synchronized to different piconets.

The total bandwidth of the Bluetooth specification is divided into physical channels of 1Mhz. Frequency Hopping occurs through changing from one of these physical channels to another, in a pseudorandom sequence. This hopping sequence is shared with all devices on the piconet.

Bluetooth devices use *Time Division Duplexing* (TDD) to access piconets, using <a href=https://en.wikipedia.org/wiki/Time-division_multiple_access>Time-division Multiple Access (TDMA)</a> as the access technique; 

![[Pasted image 20211129174911.png]]

As a result, this combination is referred to as *Frequency Hop Time Division Multiplexing Time-divison Multiple Access* (FH-TDD-TDMA).


### Bluetooth Physical Links

There are two types of physical link:
- Synchronous Connection Oriented (SCO)
	- Allocates fixed bandwidth between the point-to-point connection of both master and slave
	- The master maintains the link using reserved slots, and can support three simultaneous links.
- Asynchronous Connectionless (ACL)
	- Point-to-multipoint link between master and all slaves; only one ACL link can exist.

### Bluetooth Packet Fields

Bluetooth packets contain various fields to facilitate their use:

![[Pasted image 20211129175148.png]]

The **access code** is used to timing synchronization, offset compensation, paging and inquiries. The packet header itself identifies the packet type and carries protocol control information, and the **payload** contains user voice or data and an additional payload header, if it is present.

#### Bluetooth Packet Header Fields

- `AM_ADDR` contains the *active mode* address of one of the slaves.
- `Type` determines the type of packet:
	- For ACL:
		- Data Medium (`DM`) or Data High (`DH`), with different slot lengths: `DM1`, `DM3`, `DM5`, `DH1`, `DH3`, `DH5`.
	- For SCO:
		- Data Voice (`DV`) and High-quality voice (`HV`)
- `Flow` is a 1-bit flow control.
- `ARQN` is a 1-bit acknowledgement.
- `SEQN` is a 1-bit sequential numbering scheme.
- Header error control (`HEC`) acts as an 8-bit error detection code.

### Bluetooth Access Codes

There are three; the Channel Access Code (CAC), which identifies a piconet, the Device Access Code (DAC), which is used for paging and subsequent responses, and the Inquiry Access Code (IAC) - used for inquiry purposes.

All access codes contain a preamble, sync and trailer.

### Bluetooth Payload Format

Bluetooth packet payloads contain the following information:

- Inside the payload header:
	- `L_CH` field, which identifies the logical channel
	- `Flow` field, which is used to control flow at the L2CAP level.
	- `Length` field, which is the number of bytes of data in the payload body.

The payload body itself contains user data, and a field called `CRC` contains a 16-bit CRC code.

### Bluetooth Error Correction Schemes

There are three:

- 1/3 rate FEC (Forward Error Correction):
	- This is used on an 18-bit packet header, on the voice field in a HV1 packet. Each bit is simply sent three times over three consecutive bits.
- 2/3 rate FEC
	- This is used in DM packets, the data field of DV packets, FHS packets and HV2 packets. Each sequence of 10 bits is followed by 5 parity bits that are calculated using a (15,10) shortened Hamming code.
- ARQ is used with DM and DH packets.

#### Automatic Repeat Request (ARQ) Scheme Elements

The ARQ scheme uses 4 elements:

- Error detection: the destination detects errors and discards malformed packets.
- Positive acknowledgement is returned by the destination when receiving a good packet.
- The source retransmits unacknowledged packets.
- Negative acknowledgement is returned by the destination for packets with errors, and the source retransmits in response.


### Bluetooth Channel Control

There are two major states for channel control: **Standby** (the default state) and **Connection**, for when a device is connected. There are, however, many interim substates for adding new slaves to a piconet:

- Page: device has issued a page
	- This is used by the master.
- Page scan: device is listening for a page
- Master response: master recieves a page response from a slave node
- Slave response: slave responds to a page from the master node.
- Inquiry: device has issued an inquiry for the identity of devices in range.
- Inquiry scan: device is listening for an inquiry to be requested of it.
- Inquiry response: device has recieved an inquiry response.

A diagram detailing transisitons between states is shown below:

![[Pasted image 20211129181635.png]]

### Bluetooth Initialization

When a network begins, a potential master node identifies devices in range that may act as willing participants. It transmits an ID packet to these devices that contains an Inquiry Access Code (IAC); this process occurs in the *Inquiry* state.

Devices receive the inquiry and enter the *Inquiry Response* state, returning a *Frequency Hop Synchronization* (FHS) packet with address and timing information before moving to the *page scan* state.

#### Inquiry Procedure Details

The goal here is to discover other neighbouring devices. The inquiring node sends an inquiry message in the form of a packet containing only the IAC; this can either be a General IAC (GIAC) or Dedicated IAC (DIAC). This message is sent over a subset of all possible frequencies.

These inquiry frequencies are divided into two hopping sets, of 16 frequencies each. In inquiry state, the node sends up to $N_{Inquiry}$ sequences o