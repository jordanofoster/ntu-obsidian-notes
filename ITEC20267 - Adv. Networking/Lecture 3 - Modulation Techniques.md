# Lecture 3 - Modulation Techniques

## Signal Transmission

### Basic Setup

Signals to be transmitted are typically confined to baseband frequencies (0-500MHz). This may be higher with 5G networks. The main requirement for signal transmission is to get the frequency range superimposed into RF bandwidth; this is typically done through a process known as **Modulation**, where 1s and 0s are represented using the carrier waves themselves.

There are several considerations for modulation:

- Achieving maximum throughput with minimum bandwidth
	- This is possible, but reduces tolerance for interference
- Minimum probability of symbol error
- Minimum transmission power
- Immunity from interference
	- Achieved with lower data rates

### Modulation

If a carrier wave is defined as $y$, then:
![[ModFormula.png]]

Other combinations such as QAM (which combines amplitude and phase modulation) exist for extra comms capabilities.

#### Amplitude-shift Keying (ASK)

ASK is a form of amplitude modulation that represents digital bits as variation in carrier wave amplitude. In ASK systems specifically, 1 is represented by the transmission of a fixed-amplitude carrier wave at a fixed frequency, for a specified bit duration in seconds (written as $T$.)

#### Frequency-shift Keying (FSK)

FSK is a form of frequency modulation in which digital information is transmitted through discrete changes in carrier signal frequency.

FSK is commonly used for comms systems, including amateur radio, caller ID and emergency broadcasts. Its simplest form is Binary FSK (BFSK).

#### Phase-shift Keying (PSK)

PSK modulates a signal by changing the phase of a reference signal (typically the carrier wave). This is done by varying the sine and cosine inputs at a precise time. It is typically used by wireless LANs, RFID and Bluetooth comms.

In PSK, only the carrier phase defines the symbol.

##### Example of Phase-shift Keying (PSK)

In the example below, 8-PSK with eight different bits/symbol (and therefore 8 different phases) is shown: 

![[PSKEx1.png]]
![[PSKEx2.png]]
![[PSKEx3.png]]

8 bits equates to $2^3$, which is 3 bits per symbol.

#### Comparison of Modulation Techniques

FSK has twice the bandwidth of PSK and ASK; FSK and PSK tend to have better quality than ASK. All three are used in different scenarios:

- PSK is used in mobile digital mobile telephony.
- FSK is used in fax machines and radio.
- ASK is used for satellite comms.

![[ModTechComparison.png]]

#### QAM: Quadrature Amplitude Modulation

QAM is a combination of ASK and PSK. The number in front of a QAM spec signifies the number of waveforms and bits transmitted. For example;

- 8-QAM transmits 3 bits/symbol ... `000, 001, 010, 011, 100, 101, 110, 111` - $M = 2^3 = 8$.
- 16-QAM transmits 4 bits/symbol ... `0000, 0001, 0010, 0011, etc...` - $M = 2^4 = 16$.

In the below example of 16-QAM (4 bits = 1 symbol) symbols `0011` and `0001` have the same phase, but a different amplitude. `0000` and `1000` have a different phase, but the same amplitude.
![[QAMEx1.png]] 

QAM is used in many modems, such as DSL and HSDPA modems. 4-QAM (where $M=4$) is used for QPSK in satellite comms. QAM also acts as a core for WLAN standards (a, g, n, ac), Wimax, Terrestial broadcast and LTE networks (as COFDM).

### Channel Capacity

###### 1 bit
Each waveform transmits a singular bit with a value of either 1 or 0. For same signal bandwidth, the assumption is made that:

- Symbol rate (\# of symbols/second) = $N$ $symbols/sec$
- Bitrate (\# of bits transmitted/second) for **BPSK** $=$ no of bits per waveform , $1 \times symbol$ $rate = N$ $bits/sec$
- Channel capacity is therefore given in $N$ $bits/sec$

###### 2 bits

Each waveform transmits two bits (`00, 01, 10, 11`)

For same signal bandwidth, assumptions made are:

- $symbol$ $rate$ $= N$ $symbols/sec$
- Bitrate for BPSK = $2(two$ $bits) \times symbol$ $rate = 2N$ $bits/sec$ 

- Following is noted:
	- \# of bits, $M$, increases as \# of bits to transmit per symbol increases.
	- Channel capacity increases with number of symbols.

#### Shannon Channel Capacity Formula

In the presence of noise, the formula states:

$C = B\log_2{(1 + SNR)}$, where:

- $C =$ channel capacity in bps
- $B =$ channel bandwidth
- $SNR =$ Signal-to-Noise ratio

$SNR$ can be written in terms of $dB$ where $SNR_{dB} = 10log_{10}(SNR)$

#### M in Modulation

When $M$ (\# of bits) is small:
- There are fewer bits/symbol -> more robust modulation
- Lower $SNR$
- Higher tolerance to interference/distortion
- Lower spectral efficiency (less bits/s per Hz of transmission bandwidth -> lower bitrate/more bandwidth).

When M is large:
- Requires highest $SNR$
- Less tolerance to interference/distortion
- Most spectrally efficient -> higher bitrate/less bandwidth.
- More complex.

Highest bitrates will only be possible in following circumstances:
- $SNR$ is sufficiently high
- Little interference/distortion is present.

Practical implementations such as AOFDM can adaptively change modulation (M value) and coding methods to maximise bitrate for given channel conditions.

#### Adaptive Modulation

Adaptive modulation is defined as: an intelligent wireless communication that considers environmental network conditions. This understanding is used to build methodology to be adapted based on environment. Parameters used include:

- Channel Fading
- Including data rate
- Transfer power
