# Bluetooth

## Bluetooth Basics

Bluetooth was created by a consortium of various companies, including Ericsson, Intel, IBM, Nokia and Toshiba, amongst others. Bluetooth as a protocol aims to cover several scenarios, including:

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

