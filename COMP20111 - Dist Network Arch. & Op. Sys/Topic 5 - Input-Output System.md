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

Typically, when complex systems are engineered, a complex approach is taken; I/O is no different, having multiple layers for dealing with requests. Each layer will have an Application Programming Interface (API) providing access to the layer below.

#### Interrupt Handlers

![[Pasted image 20211206161953.png]]

Interrupts are a very important part of an I/O stack, and are not trivial to handle, requiring several steps:

1) Save registers not already saved by interrupt hardware
2) Set up context for interrupt service procedure
3) Set up stack for interrupt service procedure
4) Acknowledge interrupt controller
5) Copy registers from where they were saved to the process table
6) Run the interrupt service procedure to extract information from the device control registers
7) Choose which process to run next
8) Set up MMU context for process to run next
9) Load new process' registers
10) Start running the new process

### Structure of the I/O System

![[Pasted image 20211206162039.png]]

**User program:**
- Makes I/O request in a high level language
- Request translated and relayed by system calls

**I/O control system:**
- Deals with I/O related system calls
	- Device-independent software
	- Platform for installed drivers to communicate with

**Device driver:**
- Software module that manages the communication with a specific I/O device
- Converts logical I/O requests into specific commands directed to that device via communications bus (e.g. to which PCIe is connected)

**Device controller:**
- Hardware unit attached to the bus
- Provides interface between computer and I/O devices using electrical signals

**I/O device:**
- Block device transfers data in groups of characters
- Character device transfers data one character at a time

#### Device Drivers

![[Pasted image 20211206170347.png]]

The I/O system handles the following:
- The device(s) itself
- The device controller(s)
- The OS mediating the operations
- The user process that requests the operations

A device driver is used to provide detail on how the device works, and provides a standard API call for the OS to use. For each device, a different device driver would exist, as shown in the bottom part of the above diagram.

![[Pasted image 20211206170530.png]]

Each device has a device descriptor containing information about it, such as the following:

- The device identification
- The instructions that operate the device
- The current status
- The current user process (if any)

This information is used by the I/O controller.

##### Simplified Device Driver Behaviour

The device driver would undergo the following functions:

1) Check input parameters for validity, translating them to device-specific language
2) Check if device is free, waiting or blocking the process if not.
3) Issue commands to control device:
	1) Write them into device controller's registers
	2) Check after each if device is ready for next command, waiting or blocking if not.
4) Block or wait for controller to finish work
5) Check for errors, passing data to device-independent software
6) Return status information
7) Process next queued request, or block waiting for next

There are a few challenges with developing a device driver, namely:

- The driver must be reentrant, meaning it can be called by an interrupt while running.
- The driver must be capable of handling hot-pluggable devices, and device removal while running.
- Drivers are complex and they are many in number; additionally, bugs in them can crash a system.


##### Device Driver Interfacing

Device drivers provide access to specific devices.

![[Pasted image 20211206170945.png]] 

The issue is when there is no standard driver interface (see `(a)`); we need to alter the operating system to handle different system calls to drivers, and this is not possible or efficient.

The best way to handle this is through use of a uniformed device interface (see `(b)`):

![[Pasted image 20211206171105.png]]

With this change, it is easier to see different devices, as they all share the same syscall definitions.

Each device driver provides a set of functions; for example, a disk driver could have `open`, `close`, `read`, `write`, `seek`, `power on`, `power off` functions and many more. They are represented by a table of pointers to functions provided by the driver itself.

When the driver is loaded, the OS remembers the address of this table so that it can access them when receiving a syscall that necessitates device interaction.

The use of a uniformed device interface also allows consideration of device security, as they are named objects mapped to the file system itself as a named object (in the case of both UNIX and Windows), meaning permissions can be set to limit who has access to them.

### Interrupt-Driven I/O

![[Pasted image 20211206171437.png]]

Suppose we have an example scenario in which a user process requests an 8-char string, "ABCDFGH", to be sent to the printer:
- An interrupt is caused for each character sent (not very efficient)
- Additionally, the data transfer between device and memory unit is limited by CPU speed.

### Direct Memory Access (DMA)

![[Pasted image 20211206172503.png]]

Shown above is a diagram of the operation of a DMA transfer.

Although it is possible for us to access device controllers one byte at a time, it would be very slow and inefficient. Direct Memory Access solves this issue, with the DMA controller having access to the bus independent of the CPU.

There are several registers available that can be read/written to by the CPU, such as the Memory Address Register, Byte Count Register and Control Registers. However, the privileged access DMA controllers have is a severe system vulnerability and can be easily exploited; see [[Understanding DMA Malware.pdf|"Understanding DMA Malware".]]

### Buffering

A buffer is an interim memory area that holds data in transit between process' working RAM and the device itself. This helps to cope with any speed mismatch between the device, and also involves the performance of a checksum.

There are a few types of buffering:

**Output Buffering**
- Output data is transferred to an area of memory called the output buffer.
- The OS empties the buffer when full
- The process is blocked only if it tries to force an output before the system has emptied the buffer.

**Input Buffering**
- Input data is stored in an input buffer.
- The process takes data from this buffer.
- The OS fills the buffer when empty
- Processes are blocked if trying to get data from an empty buffer.

#### Single Buffering

![[Pasted image 20211206173113.png]]

The above diagram represents data input with a single buffer:

- Blocks are read into the buffer and then moved to the user's work area.
- When blocks are moved from the buffer, processing can be in parallel with transfer of the next blocks.
- Interrupts are reduced, but the device is still idle for some time.

#### Double Buffering

![[Pasted image 20211206173500.png]]

Here, two buffers are used: the process reads/writes to one, while the OS empties/fills the other. Using the concept of double buffering for data input as an example:

- One buffer can be emptied while the other is filled
- Maximises utilisation of I/O device

If the processing time is less than the transferring time, transferring data may be continuous. This can further be extended to multiple buffering; with enough buffers, continuous I/O can be always achieved.

### Error Reporting

Errors happen very often in I/O, and a similar issue is also presented in distributed systems. The OS itself needs to handle them, and there are several different classes of I/O error:

**Programming errors:**
- Could be trying to **write** from an **input** device or **read** to an **output** device
- Providing invalid buffer address or invalid driver
- Easy to handle, just return error code to parent

**Actual I/O error:**
- HW failure, such as disk error (faulty disk block)
- Should be handled by device driver to determine what to do:
	- Fix/mitigation strategy or if no idea, return to previous layer

**OS corruption:**
- Very serious error occurred which has corrupted OS data, such as critical data structure.
- Need to display error and terminate (BSoD/Kernel Panic).

### Overview of an Input/Output System

![[Pasted image 20211206181255.png]]

### I/O and Networking

![[Pasted image 20211206181452.png]]

A generalized Linux structure is as follows:

**User Space:**
- Application Layer (user program)

**Kernel Space:**
- System Call Interface (API to access layer below)
- Network Protocol/Stack (Send/Receive)
	- Socket handling (Berkeley Socket Interface)
- Network Device Driver (API to access device specifics)

**Physical Layer**
- Network Hardware (Physical Hardware/Network Medium)

#### Intefacing With The Device Driver

The Network Interface Driver has two circular queues:
- Transmission queue (TX)
- Receive Queue (RX)

These queues provide a buffer to store packets in, recieved from or to be sent to the Network Hardware layer.

If receiving packets:
- Network hardware receives packet (if containing its MAC address)
- DMA is used to put packet into RX buffer
- NIC generates an interrupt (assuming packet received)
- Network Protocol/Stack layer DMA