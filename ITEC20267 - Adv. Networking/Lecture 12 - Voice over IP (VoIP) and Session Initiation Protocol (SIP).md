# Voice over IP (VoIP) and Session Initiation Protocol (SIP)

## The Information Concept

![[Pasted image 20220131150427.png]]

It is not the *actual* message, but the likelihood of a message that relates to information - the more likely a message, the lower the information. For example:

![[Pasted image 20220131150508.png]]

Therefore, the relationship between Information and the Probability of Information $=(probability)^-1$

Can we measure information? We need a function such that:
- It is inversely proportional to probability, $P(likelihood)$.
- If we have two information, the information, $i$, adds.

This is the case if $I = \log (\frac{1}{p})$
But actually, $I = \log_{2}(\frac{1}{p})$ - The information has a pseudo-unit - the BIT.

Now to measure information, all we need to know is the probability or likelihood of a message.

Another example: what is the information in being told the card picked from a deck of playing cards?

Calculators don't typically know how to do \log_{2}, so we need to help them:

$\log_{2}X = \frac{\log_{10}X}{\log_{10}(2)} = 3.32\log_{10}X$, where $X = \frac{1}{\frac{1}{52}} = 52$

For reference, $\log_{10}$ is the default base of $\log$ when using a calculator.

### Entropy

#### The average information per message

Message sources usually have more than one message:

$I_1 = \log_{2}(\frac{1}{p_1})$, $I_2 = \log_{2}(\frac{1}{p_2})$, etc.

To get the average, multiply the information by the likelihood of the message and add them together. Given a special name Entropy, $H$:

$H = p_1I_1 + p_2I_2 + .. = p_1 \log_{2}(\frac{1}{p_1}) + p_2 \log_{2}(\frac{1}{p_2}) + ...$

$H = \sum_{k}p_kI_k = \sum_{k}p_{k}\log_{2}(\frac{1}{p_{k}})$

for reference, $\sum$ means to sum over all values of $k$.

#### Entropy Example

Entropy of a message source in a table:

| Message | Probability, $p$ | $I$ | $p \times I$ |
| --- | --- | --- | --- |
| A | 0.4 | 1.32 | 0.53 |
| B | | | |
| C | | | |
| D | | | |

## VoIP

### The Concept

- There is an increasing trend towards networks consisting entirely of IP-based devices.
- Internet is typically cheaper than the typical telco's PTSN systems
- Skype is a well-known (but proprietary) example.

Note that both traditional voice and VoIP involve digital transmission (at least in the network).

VoIP requires two processes:
- Call setup and termination (session management): to put the voice 'client' in touch with the voice 'server' and agree on protocols.
- Data transfer: to transfer voice data.

Note the similarity with traditional telephony (connection established then voice transmitted just like PTSN - connection terminated after use).

Therefore, consider the application as being connection oriented.

### Concept for VoIP Terminal or end point

- Analogue telephone adaptor
	- Adapts standard analogue phone to IP, connected to Internet (creates ringtones, bell voltages, etc.)
- IP phones
	- As standard phone, but connects directly to data network e.g. Ethernet or Wifi.
- PC-to-PC
	- Software IP phone client on host computer

All of these use the underlying IP network to transport voice - this is the big difference between VoIP and traditional telephony. Remember that traditional PTSNs use circuit switched TDM (Time Division Multiplexed) technology, and not a packet switched IP network.

#### Carrying voice data in IP packets

- Must digitize analogue voice from microphone and reverse at destination ('undigitize' the voice 'data' to give to the loudspeaker).
- Choice of codec for this can be important:
	- IP offers no guarantees of bandwidth, or that a packet will arrive in a timely fashion, if it arrives at all.
	- Data is routed by packet switching, instead of the circuit switching of traditional telephony.
	- Therefore, a codec that can handle packet losses is good, such as ILBC (Internet low bit-rate codec)

If we try to fill an IP packet destined for an Ethernet frame payload of roughly 1500 bytes and 8bit sampling (we need ->64Kbps throughput) - we send one packet every 25ms.

#### VoIP Codec

Typical parameters used for coding VoIP voice using ILBC as an example:
- Sample rate: 8kHz
	- 30ms worth of samples (=240 samples) per packet

Reducing the bitrate using Compression:
	- Based on *Linear Predictive Coding:*
	- End up with 50 bytes/30ms frame \[=>13.3kb/s\]
	
Note the coding delay of 30ms before any network delay is added.

As a result, you end up with small packets, with 50 bytes of application data. This is not very efficient as the packet/frame headers are a significant portion of the transmission.

#### Packet transfer: reordering and timing

The coded voice packets need to be made ready for transport over the IP network. The decoder needs the coded data in the right order and the right time. While we're at it, we should try to maximise bandwidth efficiency by minimising overheads.

We would do this by sending data over a TCP connection to make sure things are in the right order and no packet losses are sustained, but it makes sure every segment gets there using retransmissions if neccessary. This is fine if none are needed, but because we have to wait and we're trying to have a conversation, delay is a killer (only 150ms is the maximum acceptable delay.) In addition, the 20 byte segment header is significant.

Since TCP is a problem, we go for using UDP instead.

##### UDP usage issues

UDP is a connectionless, best effort protocol with only an 8 byte header; they can arrive out of order and with no timing constraints (whereas TCP has to retransmit). As a result, we use RTP (Real-time Transport Protocol) instead.

#### RTP

This is the real time transport protocol, used when data needs to be presented at the right time, even when the packet arrival has variable delay. Packets themselves need to be in the right order - IP doesn't have a means for doing this; TCP might have an implementation, but it gets delayed with packet losses.

RTP gives data proper timing and order by having a sequence number and timestamp in its protocol header, and RTP PDUs are transported in UDP datagrams over IP. It is defined in RFC3350.

## SIP

The Session Initiation Protocol is an application-layer protocol that enables voice (or more generally, multimedia) streams to be connected. The protocol itself has lots of detail, as defined in RFC 3261.

### What SIP Does

SIP has five areas that support establishing and terminating multimedia communications:

1) User location - locating end-user devices, such as finding an IP address.
2) User availability - determination of willingness to engage (is user busy?)
3) User capabilities - what sort of media can be used (e.g. voice/video, codec parameters)
4) Session setup - Establish session parameters at both ends and indications such as 'ringing'
5) Session management - transfer and termination of sessions, modifying session parameters 

#### SIP phone

![[Pasted image 20220131161321.png]]

##### SIP Phone Registration

1) Phone boots up
2) Registers with SIP registrar (location database) uses DNS to resolve registrar's IP address
	1) Sends SIP message indicating own user address (user@domain e.g. like e-mail) and current IP address.
	2) e.g. taw@ip-phone.org is at 175.248.98.45
3) Registers again when time expires or new location (=new IP address)






