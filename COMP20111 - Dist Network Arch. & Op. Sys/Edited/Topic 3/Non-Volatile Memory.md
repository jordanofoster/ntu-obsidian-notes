# Non-Volatile Memory

## Hard Drives

#isys20231-nda/topic-4 

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
2) BIOS per