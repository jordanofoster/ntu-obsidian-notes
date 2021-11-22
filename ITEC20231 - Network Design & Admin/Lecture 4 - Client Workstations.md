# Client Workstations

Workstations/Client machines are any devices that actual users sit at and use. Operating systems that workstations run include Windows 10, Linux, and OS X. Some legacy systems still exist as well.

An important feature for workstations is that they have to be able to communicate with servers and use their services - although they can be used standalone.

They are also much more likely to have issues, as the user is directly involved. 

Total Cost of Ownership (TCO) must be considered when buying one; this is a financial estimate that includes the direct and indirect costs of a product or system, including purchase of a particular asset, or operating costs over its lifespan. It is basically a method of assessing the long-term value of a purchase to a company or individual.

## New Workstations

Workstations may already be bought with an operating system on, but generally new OSes are installed in most instances:

- Stock OS may be feature-incomplete, or not corporate standard (Home instead of Enterprise, or older version needed).
- User preference may be considered, but only if the corporation allows it.
- Some workstations need multiple boot options, or are bought bare (where volume licencing is used).

Generally speaking, consistency is desired (i.e. starting from a known state), and the process of setting a new one up boils down to three basic tasks:

- Loading initial system software/applications
- Updating system software/applications
- Configuring network parameters

Each option will have an effect on TCO, however.

### What new workstations come with

Computer typically come with the OS preloaded:
- Windows machines come with basic versions of standard tools (e.g. word processor, email, etc...)
	- There is an expectation on the user to pay for the Office suite, and/or an exchange server within a corporate environment.
- Linux comes with a full set of free standard tools.
- Linux offers a complete turnkey system.

## Life and Death of a Workstation

Below is Evard's lifecycle of a machine and its OS:
![[EvardMachineLifeCycle.png]]

**New** refers to a completely new machine. **Clean** machines are those on which an OS has been installed, but no localizations performed.
**Unknown** refers to misconfigured and/or out of date devices.
**Off** - retired and powered off machines.

Computers are only usable in a configured state; entropy occurs as workstations are modified over time due to failed installs, malware, and inappropriate software. As such, procedures to bring devices back to configured state as efficiently as possible are required.

## User Expectations

Workstations must provide:

- Corporate standard word processing packages, with standard corporate setup (e.g. foreign language support if required by business).
- Allow use of standard email package with no extra user effort.
- Business specific software is already installed.
- Corporate purchased anti-virus, anti-spam & malware software is already installed.
- Web access is present and appropriate.

The workstation must not:

- Force users to do anything but log on to begin work.
- Allow users to install their own packages, unless authorised.
- Encourage users to keep files locally; whereever possible, encourage sending work to file servers instead.

It may be worthwhile to provide new users with a do/don't list when obtaining a new workstation.
 
##  File System Formats

![[FileSysFormats.png]]

### File Systems Layout

A drive is divided into partitions/volumes, each which hold an independent file system.

![[FileSysLayout.png]]

### File Block Allocation Methods

![[FileBlckAlloc.png]]

File Block Allocation keeps track of which files map to which block on a physical drive. Different allocations schemes include:

- Contiguous allocation, used in CDs
- Linked list allocation (non-contiguous)
- Linked list with file allocation table, used in DOS/Windows
- i-nodes, used in UNIX

Blocks are subdivisions of mass storage (such as pages and frames for main memory); originally related to disks.

#### Example

![[FileBlckAllocEx1.png]]

Using a linked list, files are stored on the root directory.
`cmd.com` starts in cluster 4;
position 7 is read in data.
cluster 10 is read in data.
cluster 6 is reads in data.
File contents are built up.
FFFF is added for the end of the file.

#### File Systems in Unix using i-nodes
![[FileSysUnixINodes.png]]

The i-node contains a number of direct pointers to disc blocks. Typically, 10 *direct* pointers exist. In addition, three indirect pointers exist, which point to further address blocks, which eventually lead to disk data blocks. The first of the three is a single level of interdiction; the next is a double indirect pointer and the third is a triple indirect pointer.

## Hard Disk Geometry

![[HDGeometry1.png]]
![[HDGeometry2.png]]

Hard disks usually have a number of platters contained within. Each side is used and will have its own read/write head. Each surface of a platter will contain a number of tracks and sectors.

### Magnetic Disks

![[MagDiskSector.png]]

Above is an example of two sectors on a portion of a disk track. The preamble is used to sectup a sector (as formatting a disk sets the preamble to contains cylinder/sector #'s) and for synchronising the read/write head. ECC, or Error Correcting Code, also exists in order to see if data is correct.

![[HDDSSDComparison.png]]

## Integrating Linux

Considerations for integrating linux as a system include:

- Authentication against an active directory server
	- Requires setup of `kerberos` package using `apt-get`
		- `kerberos` is configured with a realm for domain
			- Keyserver and domain details are configured
		- A new `kerberos` ticket is generated
	- Setting up SMB file access via Samba
		- `smb.conf` configured with realm details
	-  Configure `nsswitch.conf`
		-  Add WINS, DNS and BIND information
	- Join domain.
	- File shares etc still have to be set up  

It is easy to add windows workstations to an Active Directory domain, but less so for other operating systems.