#COMP20111-DNAOS/memory-management
# Memory Management

## Current position (Windows)

![[Lecture3CurrentPos.png]]

## Memory Hierarchy Pyramid

Computer systems are typically composed of a layered memory system; higher layer correspond to faster devices, but have:

- Lower capacity
- Require more power, and thus generate more heat
- More expensive
- Volatile, meaning information does not persist after power-down

In contrast, lower layers correspond to higher capacity memories, which are:

- Slower
- Cheaper
- (At lowest layers) Non-volatile

The image below visualises various types of storage in the pyramid:

![[MemoryHierarchyPyramid.png]]

### Types of Memory

#### Primary/Volatile

##### Processor registers

These are small and extremely fast memory units that reside inside the CPU, typically in the form of individual containers for single values. They are typically referred to by name (i.e. individually identifying codew) instead of address (as is the norm for other types of memory).

They are used primarily for arithmetic operations and are manipulated and/or tested by machine instructions. There are two types of processor registers: **generic** and **specialised.** 

![[GenericSpecialisedRegisters.png]]

Generics are mainly used to allow the CPU to temporarily store data to use as function parameters, alongside the storage of function output data. Specialised registers are manipulated mostly in the same pattern, but are named due to their used for specific purposes (e.g. program counter).

###### Cache Memory
![[CacheDiagram.png]]
This is small, fast memory used to reduce average time/energy cost to access data from main memory. It also resides within the CPU, being an intermediary between main memory and processor registers. Modern computers typically have a sub-hierarchy of cache memories categorised from fastest-to-slowest from lowest-to-highest (e.g. L1, L2, L3, L4 etc). A real-world example of a CPU's cache memory is shown below, via CPU-Z:

![[CPU-ZExample.png]]

##### Main Memory RAM

A diagram connecting main memory to CPU registers/cache is shown below:

![[MainMemoryRAMDiagram.png]]

#### Secondary/Non-volatile

##### Hard Drives

Pre-existing notes on these are present in Lecture 4 of the *Network Design & Admin* module. The relevant section has been linked below:

![[Lecture 4 - Client Workstations#Hard Disk Geometry]]

##### Flash ROM
![[FlashROMDiagram.png]]
Flash ROM is used in the system boot process when powering on the PC, as follows:

1. Motherboard BIOS initializes its registers and power management system.
2. Bios performs following procedures:
	a. self-diagnostic test (known as POST, or *power-on safe-test*)
	b. Boots the BIOS of all subsidiary boards
	c. Begins comms procedures with basic peripherals
3. Motherboard BIOS initialises the bootstrapping sequence:
	a. Copies secondary bootloader to RAM
	b. Secondary bootloader (e.g. GRUB, LILO, NTLDR, etc.) waits a few seconds for user choice
	c. Secondary bootloader loads the chosen OS to RAM and relinquishes control.
	
## Memory Management

### Concepts & Aims

Similarly to how processes share a CPU, they also share physical memory. Main memory is one of the most important resources in a computer system; instructions are fetched from it to the processor for execeution, and the memory is large enough to store several running processes at once.

![[MemMgmtDiagram.png]]

**Memory management** aims to provide memory space for concurrent processes, and to take advantage of the **locality of reference** - that is, transferring code/data estimated to be used next from the bottom of the pyramid to the top. It also protects processes from one another, relocates memory to new processes, and overall intends to make the addressing of memory space transparent by providing **memory abstraction** to developers.

### Abstraction
![[AbstractionDiagram.png]]
Similarly to how process management involves the creation of an *abstract CPU* that runs processes seemingly concurrently, memory management systems provide *abstract memory* that allows for co-existence of processes inside of physical memory.

#### Not using abstraction

In early mainframe computers, every program had access to physical memory; the model presented to the programmer was a set of addresses from 0 to max, with each address corresponding to a cell of a fixed bit length. Naturally, this has its disadvantages: it is **not possible to have two programs running at the same time** as when another program is loaded over another, the instructions of the currently running process are overwritten. Concurrency can be achieved with threads - but oftentimes unrelated programs must run at the same time (a situation not solvable with threads themselves, as they have a parent process).

![[NonAbstractionDiagram.png]]

Model `(c)` of the above diagram was the memory layout used by MS-DOS for the part of the OS stored inside the BIOS.

##### Referencing Physical Memory

![[ReferencingPhysMem.png]]

As stated before, this has a few drawbacks, but in an OS context, users can address the memory directly, trashing the OS intentionally and/or accidentally - as shown in models `(a)` and `(b)`. It can also be difficult to have multiple programs running at once, via a context switch.

The obvious solution here is that users should not be able to reference physical memory directly, and that is where the next section comes in:

### Address Spaces

Address spaces are a set of address locations that can be used to reference specific parts of physical memory.

#### Logical Address Spaces
![[LogAddrSpaces.png]]
With this system, programmers can have their programs refer to their own *logical address space* - a clear improvement, but the challenge ends up being how to distinguish that the *same logical address* seen by *two different processes* corresponds to *two different physical memory locations.*

Through a procedure known as **process loading**, programs must be transferred to main memory for execution via the **loader**. Several other issues need to be addressed, however: 

- We cannot be certain where the program has been loaded in physical memory
- The code is unable to refer to fixed memory addresses (a sometimes desirable trait)
- Machine instructions should not directly be able to access physical address space.

As a result, our program-specific (*logical*) addresses **must be converted** to physical addresses. This process is done via a hardware device known as a **Memory Management Unit** (MMU), which uses registers to record partition locations.

### Base and Limit Registers

![[BaseLimitRegs.png]]

**Base registers** store the start address of a logical partition; **limit registers** store its length. Whenever processes reference memory, the base register is used as a *relocation register;*  in addition to this, the address is checked to ensure it is within the range specified by the partition.

#### Memory Protection & Relocation

The **value of the base register** is added to the *logical address* to map to a *physical address* in a process known as **relocation.** Logical addresses greater than the **value of the limit register** point to an invalid memory address location, which **acts as a form of memory protection.**

![[MemProcReloc.png]]

The *address part* of the machine instruction interpreted is used as an offset from the *base address.* To provide an example using the image above:

- Base address is `101`
- Machine instruction is `JMP 5`
- The result is that there is a jump to `101+5 = 106`.
- Therefore, *logical* `JMP 5` -> *physical* `JMP 106`

##### Buffer Overflow Attacks

![[BufferOverflowAttk.png]]

Shown above is the following scenario:

Figure `(a)`: Main program is running
Figure `(b)`: After procedure `A` is called...
Figure `(c)`: Buffer overflow occurs, shown in grey.

An example C program that would cause such an error is as follows:

```
int position;
char buffer[2000];
position = 10000;
buffer[position] = 0;
```

### Fixed Partition Memory

![[FixedPartMem.png]]

With this structure, memory is divided into several partitions of *fixed size* - not all fixed partitions are the same size, but once created cannot be shrunk or grown in length. Each process is then given its own partition to work with. 

#### Advantages of Fixed Partition Memory

- Compatible with process co-existence in memory, allowing multiprogramming.
- Easy to implement
- Allows fast context switching

#### Disadvantages of Fixed Partition Memory

- Restricts the number of simultaneous processes.
- Each partition has unused space, leading to *internal fragmentation.*
	- This, naturally, wastes space
- And as a result, there may not be a big enough partition to fit a process.

### Dealing with Processes of Varying Size

![[VarSizeProc.png]]

So far, the assumption has been made that processes have a fixed size and that OSes always exactly allocate that memory, but this is obviously not true; some processes may try to grow, for example by increasing the size of an array.

In some cases, this is an easy fix - if a hole caused by internal fragmentation is adjacent to the process, it can be allocated, allowing the process to simply *grow* into that hole. 

But if the system is out of memory or no holes are big enough, then other processes must be swapped out to make space, or the process trying to gain more memory needs to be suspended

#### Variable Partition Memory

![[VarPartMem.png]]

Through this, each process is allocated the *exact* size of memory space required; processes are then loaded into contiguous memory slots until full. This has advantages:

- No internal fragmentation occurs
- When processes terminate, their space is freed up
- Adjacent fragmentations can be merged
- And the number of parallel processes is not fixed.

However:

- This model assumes the memory manager knows how much memory a process needs...
- And can cause holes to form outside of partitions; known as *external fragmentation.*

This can be resolved by the following:

##### Compaction

![[Compaction.png]]

When external fragmentation occurs, programs are physically moved in memory to close holes up. This does however have a **significant drawback of heavy overhead** and as such is not commonly performed.

##### Swapping

As the [[MemoryHierarchyPyramid.png|memory hierarchy]] shows, memory is not infinite; in practice, the total amount of RAM needed by all processes running in a system is often much more than is actually available. To save space, idle processes are typically stored on secondary memory, so that they don't take up precious main memory when not running. The allocation of memory changes as processes are loaded and unloaded from main memory to/from secondary memory.

![[SwappingDiagram.png]]

One simple strategy of doing this consists of bringing in each process in its entirety, executing it for a period of time and then returning it in its current state to mass storage, a process known as *Swapping*. It acts as an analogous concept to context switching with processes, but with memory management instead.

This can cause problems, however; when memory is assigned dynamically via swapping, it must be managed by the OS, typically by keeping track of free space.

### Managing Free Space

![[FreeSpaceMgmt.png]]

There are two methods of managing memory usage and free space: bitmaps (shown above in figure `b`) and free lists (shown in figure `c`).  [[Topic 4 - File Management#Tracking Free Space | Both methods are mentioned more thoroughly in Topic 4 (File Management).]]

#### Placement Policies

![[LinkedList.png]]

In free lists (shown above as a form of linked list), we have a list of processes and memory holes sorted by address. From this, several algorithms known as **placement policies** can be used to allocate memory for new processes; these define our reaction to a situation where more than one compatible hole for a new process is present in memory. They are listed as follows:

##### First Fit
![[FirstFit.png]]
In this policy, we search from the beginning to find the **first hole big enough** for our new process. The hole is then **split into used and unused space.** Statistically speaking, though, we are unlikely to have a perfect fit with this method, meaning that we may end up generating *more holes* - it is *fast,* though; primarily because we're attempting to search for a fit as little as possible.

##### Next Fit

![[NextFit.png]]

This acts as a **variation of *[[Topic 3 - Memory Management#First Fit|First Fit]]*** - where the **last time a suitable hole was found** is also kept track of. The policy uses this information to begin its search for a fit from the place it last left off, with the hope of speeding up search times by skipping tiny holes that cannot fit most processes. Unfortunately, it is often **not very successful.**

##### Best Fit
![[BestFit.png]]

This policy searches the **entire list from beginning to end** in an attempt to find the hole that is **closest to actual needed size** rather than break up bigger holes hich might be needed later. 

In theory, this has the advantage of not wasting memory - but practically speaking, we end up **generating many tiny, useless holes** compared to *[[Topic 3 - Memory Management#First Fit|First Fit]]*, which generates larger holes on average that can also be used by other processes. One definite disadvantage on top of this is **how slow it is** as the entire list must be searched.

##### Worst Fit

![[WorstFit.png]]

Opposite of *[[Topic 3 - Memory Management#Best Fit|Best Fit]],* this policy selects a hole which leaves the **maximum amount of unused space** in an attempt to solve the problem of creating smaller holes.

The idea being that if a hole is big enough, there are more **possiblities to fit other processes** than smaller holes, so *technically it isn't a waste of memory space* - but realistically, also not very successful.

##### Quick Fit

![[QuickFit.png]]

This policy has the idea of using a table of lists, where each entry points to a different list corresponding to most commonly requested sizes (such as one list for larger holes and another for smaller holes). 

This is *extremely fast* but at the cost of overhead required to maintain all these extra lists.

###  Virtual Memory

So far, the assumption that processes are stored in RAM as a whole has been made - a method known as *contiguous memory allocation.* This is unnecessary however when most of the time, the full process does not need to be in memory - only a part of it is *actually needed.* Some processes are entirely too large to even fit in main memory in the first place, as well.

The natural solution to this is to store part of the process on secondary storage, loading these parts to main memory when required. This is done via the use of *virtual memory* - a memory management technique that provides an idealised [[Topic 3 - Memory Management#Abstraction|abstraction]] of storage resources that are actually available on the machine itself.

Virtual memory removes having to deal with secondary memory for swapping purposes from users and developers by giving the illusion of a very large pool of main memory, thereby hiding the [[MemoryHierarchyPyramid.png|memory hierarchy]] from them.

#### Interplay between Virtual Memory and Swapping

Swapping allows the use of multiple processes to run where the **sum of their sizes** is larger than overall RAM size. Virtual memory allows the running of singular processes larger than RAM size - both act as two sides of the same coin, and virtual memory is implemented via **[[Topic 3 - Memory Management#Paging|paging]] and [[Topic 3 - Memory Management#Segmentation|segmentation]].**

#### Paging 

![[PagingDiagram.png]]

Paging is a memory management mechanism that allows physical address space of a process to be **non-contiguous.** This is done by dividing physical memory into blocks of **equal size** called **frames** - and dividing [[Topic 3 - Memory Management#Logical Address Spaces|program/logical address spaces]] into blocks of the same size, known as **pages.**

Pages are loaded into the available frames as the processes they contain are executed; this acts as a good solution to external fragementation.

##### Process of forming pages

![[FormPageProcDiagram.png]]

Each [[Topic 3 - Memory Management#Logical Address Spaces|logical address]] is formed as $(p,d)$ - where $p$ is the process page number, and $d$ is a displacement - or *offset* - within that page.

Each process has a *page table* - which records the frame number for each process page. This is, again, implemented via hardware; specifically the [[Topic 3 - Memory Management#Logical Address Spaces|Memory Management Unit (MMU)]], responsible for mapping logical addresses to physical addresses.

###### Example 1:

![[FrmPgProcDiagramEx1.png]]

- Given a 16-bit program address of `0100 0000 0110 0100`:
	- Process page number (4-bits) is `0100` or number $4$
	- Displacement (12-bits) is `0000 0110 0100`

- The physical address is as follows:
	-	`1100 0000 0000 0000` + `0000 0110 0100` = `1100 0000 0110 0100`$_2$

###### Example 2:

![[FrmPgProcDiagramEx2.png]]

- Given a 16-bit program address of `0101 0110 0110 0101`:
	- Process page number (4-bits) is `0101` or number $5$
	- Displacement (12-bits) is `0110 0110 0101`

- The physical address is as follows:
	- `1011 0000 0000 0000` + `0000 0110 0110 0101` = `1011 0110 0110 0101`$_2$

##### Page Tables

The purpose of one of hese is to **map virtual pages into page frames.** The layout of one is highly machine dependent, although there are some important common fields:
1. **Page frame**
	- This is the most important field, and outputs the number of the frame.
2. **Present**
	- This records whether the page is present in *main* or *secondary* memory.
3. **Modified**
	- This records whether the page has been modified since its last loading.
		- This is also known as a **dirty bit** - if it is true (`1`), the page needs to be copied back to the disk.
4. **Protection**
	- Records what kind of access is permitted.
		- (Read/Write/Execute)
5. **Referenced** 
	- Set by the OS when the page is used. 

##### Page Fault Handling

*Page faults* occur when a specific part of an executing process is not in main memory at **the moment it is needed by the CPU.** These cause [[Topic 2 - Concurrency#Interrupts|an interrupt]] that goes as follows:

1. The OS selects an existing page frame.
2. This page's **modified** bit is checked to see if modifications have occured.
3. If it has (`1`), then write the contents back to the disk.
4. Fetch a new page from the disk, replacing the old page in the frame.
5. Update the page/frame mappings and restart the trapped instruction.
	- Mark virtual page as unmapped via the *present bit* and update the address to that page with a new translation to physical memory.

When processes terminate, all of their pages are released from virtual memory.

##### Page Replacement

In this process, it must be decide which page has to be removed from RAM and placed within mass storage - in an efficient manner with minimal overhead. *Thrashing* should particularly be avoided; this is when the CPU ends up spending more time swapping pages than executing the processes they contain.

As a result, the following must be considered:

1. Modified pages must first be saved, whereas unmodified pages are simply overwritten.
2. It is preferred to not replace often used pages in and out of main memory.

Information to determine as such is derived from the page table in the form of [[Topic 3 - Memory Management#Page Tables|bits]].

Optimally, pages that are **not needed for the longest time in the future** are replaced, but this is infeasible for the following reasons:

1. It is impossible to know the future of a program's runtime
2. Thus, it is impossible to know when a specific page will be needed next.

It is still useful to benchmark page replacement alogirthms based on observed data, to act as a retrospective *what if* analysis of sorts.

###### "Not Recently Used" Page Replacement
This method uses the **reference** and **modified** bits from a page table to collect usage statistics; pages are classified as follows:

- Class 0, `0 0` -> Not referenced/Not modified
- Class 1, `0 1` -> Not referenced/Modified
- Class 2, `1 0` -> Referenced/Not Modified
- Class 3, `1 1` -> Referenced/Modified

Pages from the **lowest nukmbered non-empty class** are removed; a [[Topic 2 - Concurrency#Interrupts|timer interrupt]] clears the reference bit to distinguish between pages recently referenced, and those not.

This method has very low overhead and is easy to implement, but evidently is not an optimal way of doing things.

###### FIFO Page Replacement

A list of all pages currently stored in memory is maintained inside of the memory itself. The **most recently arriverd page** is located at the tail of the list, with the **least recently** at the head. When needed, the head page is removed; the incoming page is added to the tail of the list.

The oldest page may still be useful, however - and as a result, this method is rarely used.

###### "Second Chance" Page Replacement

This is a variation of FIFO that avoids accidentally replacing a heavily-used page due to age, by checking the reference bit of the oldest page first:

![[SecondChancePgReplacement.png]]

If the bit value is `0`, it is replaced much like the normal FIFO algorithm, but otherwise, its bit is cleared and the page is moved to the end of the page, resetting load time. The search then continues onto the next page, as shown below:

![[SecondChancePgReplacement2.png]]

This clearly still has the disadvantage of potentially unneccessarily moving pages around the list, but at minimum this method is a big improvement over FIFO.

###### Clock Page Replacement

Again, much like FIFO, but pages are maintained on a circular list:

![[ClkPgReplacement.png]]

This model helps to avoid the unneccessary movement of pages caused by both FIFO and Second Chance; the pointer points towards the oldest page and checks the reference bit again, without needing to actually move any pages about. A far more realistic approach.

###### "Least Recently Used" Page Replacement

This method operates on the likelihood that heavily used pages will continue to be heavily used, by swapping out pages that have been left unused for the longest amount of time.

This has excellent performance, but requires the maintenance of a linked list of **all pages in memory** - with the *most recent* at the front and *least recent* at the rear. The list must be updated/maintained with every reference to memory, and the referenced page must be moved to the front of the list.

It goes without saying that such an implementation is both difficult and time-consuming to produce.

###### "Not Frequently Used" Page Replacement

Again, how often a page is used is tracked here, through an associated counter for each page in the frame, initially set to `0`. 

1. At each clock interrupt, the OS scans all pages in memory
2. For each page, the **reference** bit is added to the associated counter.
	- As a result, counters keep track of how often each page is referenced.
3. When page faults occur, the paged with the lowest counter value is replaced.

With this method, **almost full utilisation** of physical memory is achieved, and programs with address space larger than physical memory can be executed. There is also **no external fragementation.**

All of this does come at various costs, however:

- Some internal fragmentation occurs. A process may not use memory in *multiples* of a page - for example, the last page usually does **not use** the entire page size.
- Tuning page size for this method is tricky:
	- Smaller page sizes cause **less internal fragementation** but require **larger paging tables**
	- Larger page sizes cause **more unused programs** loaded into memory, but as a result **smaller paging tables** are required.

One page table for each process may consume a lot of physical memory, and this method does not divide pages into unit to support logical divisions of programs.

#### Segmentation

Segmentation is a memory management scheme that works with the **logical user-view** of programs. Each program is split into **variable-size chunks** called **segments** according to the logical structure of the program:

![[SegmentationDiagram.png]]
- For example, a C compiler may generate 4 segments; a symbol table, a parse tree, a stack and a constants table, all of different sizes.

Memory is allocated to processes segment-by-segment, in non-contiguous areas of physical memory. Each segment has its **own address space.**

###### Advantages & Disadvantages

Segmentation allows the logical divison of programs, and segments themselves can grow and shrink dynamically and independently of one-another (e.g. stack and heap). Segmentation also supports [[Topic 3 - Memory Management#Protection Sharing|both protection and sharing]].

But segments are typically much larger than pages and may waste space - and tend to be prone to external fragementation.

##### Protection & Sharing

Segmentation **aids both of these:**
- **Protection** is achieved by assigning different modes (*read/write/execute*) to each segment, and checks that references to memory do *not exceed segment length.*
- **Sharing** refers to a shared segment referenced by multiple processes, such as libraries.

#### Comparison of Paging & Segmentation

[[Topic 3 - Memory Management#Paging|Paging]] is useful to allow more address space without requiring more *actual physical memory.* Memory is divided in a way that is **transparent to the user**, but pages are of a **fixed size** - this is offset by having **no external fragmentation.**

[[Topic 3 - Memory Management#Segmentation|Segmentation]] allows programs to be broken up into independent [[Topic 3 - Memory Management#Logical Address Spaces|logical address spaces]], and allows logical division of a program which is **visible** to the user (**useful for programmers**) - segements are of a variable size (which is nice for efficiency), but this can **generate memory holes.**

#### Segmentation with Paging

Typically, segments are larger than pages. This can present a problem if a segment is **larger than physical memory.** We resolve this by **mapping segments into page frames** via a process known as *paging segments* - this occurs as follows:

- Each segment is assigned with a page table.
- In theory, this achieves the best of both worlds:
	- **Avoids external fragmentation**
	- **Aids sharing & protection**
	- **Supports a user-view of the program**

As a result, this is roughly equivalent to what is used in modern systems today, such as x86, ARM, etc.

## Distributed Shared Memory

![[DistSharedMem.png]]

In single computer systems, there are a number of discrete computing resources available to the system, such as the CPU, Memory, Bus, I/O, etc. In distributed systems, each node has its own set of resources which are linked together to form a whole.

Memory is one such resource which needs to be organised to be used, be it individually or collectively.

Distributed Shared Memory (DSM) is based on **message passing** - a concept learned about more in [[Lecture 8 - Procedural & Physical Controls | Topic 8]].