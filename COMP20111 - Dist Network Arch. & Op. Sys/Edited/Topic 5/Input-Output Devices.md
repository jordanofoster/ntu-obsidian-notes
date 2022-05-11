#comp20111-dnaos/topic-5
# Input-Output Devices

![[Pasted image 20211206150649.png]]

- Peripherals can either give inputs or outputs
	- Device controllers connect them to the PCI bus.
		- They fall into one of the following two devices:
			- [[Block Devices]]
			- [[Character Devices]]

## Goals of the I/O Layer

- **Device Independence**
	- Allow [[Programs|programs]] to access I/O devices *without* specifying or knowing about them in advance.
		- Example include disk read/write, 