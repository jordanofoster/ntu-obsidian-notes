# Input/Output and networking

## Current Position (Windows)

![[Pasted image 20211206150616.png]]

## Input/Output Devices

![[Pasted image 20211206150649.png]]

Devices can be either input or output devices, and device controllers are used to connect them to the PCI bus. They fall into one of the following two categories:

###### Block Devices

Block devices store information in addressable blocks, and can write to blocks independently of other blocks. Examples of block devices include hard disks and flash drives.

###### Character Devices

With character devices, a stream of characters is sent or received. They are *not* address based, and include devices such as printers and mice.

### Goals and services of the I/O Layer

**Device independence**
- allow programs to be written that can access I/O devices without specifying them or knowing about them in advance
	- Examples include reading a file from a disk, be it floppy/magnetic/CD-ROM/etc
- There is no need to modify the program if a new device comes in.

**Uniform naming ("Mounting")**
- Abstract naming spaces independent of physical devices.
	- Naming should be a string and/or integer ID, again without device awareness

**Error handling**
- Lower layers must always try to handle the error before upper levels.
- Controller hardware should attempt to correct the error first; if it cannot, then driver software should take the reins (e.g. by reissuing the command, etc).
- Upper levels can remain unaware of errors handled at lower levels.

**Synchronous vs. asynchronous transfers**
- Most physical I/O is asynchronous (interrupt-driven)
- O/S should make it look synchronous (blocking) to processes

**Buffering**
- Decouple transfer rates and insulate data from swapping

### Input/Output Software Layers

![[Pasted image 20211206151541.png]]

Typically when complex systems are engineered, a complex approach is taken; I/O is no different, having multiple layers for dealing with requests. Each layer will have an Application Programming Interface (API) providing access to the layer below.

#### Interrupt Handlers

Interrupts are a very important part of an I/O stack, and 