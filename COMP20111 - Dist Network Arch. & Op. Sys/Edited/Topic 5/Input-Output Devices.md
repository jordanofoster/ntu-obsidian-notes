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
		- Example include disk read/write
			- Whether floppy/magnetic/CD-ROM/etc
	- No need to *modify the [[Programs|program]]* if a new device is added
- **Uniform naming ("Mounting")**
	- *Abstract* naming spaces *independent* of physical devices
		- Should be a string and/or integer ID
			- [[Programs]] do not require *device awareness*
- **Error Handling**
	- Lower layers must *always* try to handle errors *before* upper layers
		- Controller hardware attempts to correct error first
			- If it can't then driver software does:
				- i.e. reissuing commands, etc.
	- Upper layers *unaware* of low-level errors that are handled.
- **Synchronous vs. Asynchronous Transfers**
	- Most physical I/O is *asynchronous* ([[Interrupts|interrupt]]-driven)
	- O/S makes it *look* synchronous (using blocking) to [[Processes|processes]]
- **Buffering**
	- *Decouple* transfer rates
	- insulate data from [[Swapping|swapping]]

## I/O Software Layers

![[Pasted image 20211206151541.png]]

