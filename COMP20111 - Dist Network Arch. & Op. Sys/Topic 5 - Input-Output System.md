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
- Allow programs to be written that can access I/O devices without specifying them or knowing about them in advance
	- Examples include reading a file from a disk, be it floppy/magnetic/CD-ROM/etc
- There is no need to modify the program if a new device comes in.

**Uniform naming ("Mounting")**
- Abstract naming spaces indepemnde