#comp20111-dnaos/topic-3 
# Non-Volatile Memory

## Why use Non-Volatile Storage? #comp20111-dnaos/topic-4

- Sometimes, it is desirable to store data for later use and further processing.
	- This should happen even after shutdown, predicted or otherwise:
		- Critical errors, crashes or otherwise forced terminations.
- [[Volatile Memory]] (and by extension, [[Volatile Memory#Random Access Memory RAM|RAM]]) is *insufficient*:
	- Information in [[Processes|process]] [[Memory Management#Logical Address Spaces|address space]] is lost when the process terminates
	- Capacity *too limited* to handle *all data at once* for most applications
		- This is why [[Virtual Memory]] exists.

## Hard Drives #isys20231-nda/topic-4 

- Hard disks usually contain a number of platters:
	>![[HDGeometry1.png]]
	- Each side of the platter has its own read/write head.
- Each platter surface contains a number of tracks/sectors:
	>![[HDGeometry2.png]]
	
### Magnetic Disk Geometry
- Below shows two sectors on a portion of a *disk track:*
	>![[MagDiskSector.png]]
- The *preamble* is used to set up a sector and to synchronize the read/write head.
	- For sectors, formatting a disk sets the preamble to contain cylinder/sector numbers.
- *Error Correcting Code* (ECC) also exists to check data for errors.

### Image Comparing HDDs and SSDs

![[HDDSSDComparison.png]]

## Flash ROM

![[FlashROMDiagram.png]]
This is used in the *system boot* process when powering on the PC:
1) BIOS initializes registers, power management system
2) BIOS performs following:
	1) *Power-on Safe-test* - POST
		- A form of self-diagnostics.
	2) Boots BIOS of all subsidiary boards
	3) Initiates communications with basic peripherals.
3) BIOS begins bootstrapping sequence:
	1) Copies *[secondary bootloader](https://en.wikipedia.org/wiki/Bootloader#Second-stage_boot_loader)* to [[Volatile Memory#Random Access Memory RAM|RAM]]
	2) Bootloader waits on user choice
	3) Bootloader puts chosen OS in RAM, relinquishes control.