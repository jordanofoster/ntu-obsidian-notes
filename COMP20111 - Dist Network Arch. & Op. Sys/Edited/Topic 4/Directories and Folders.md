#comp20111-dnaos/topic-4 
# Directories and Folders

- Most filing systems group files using these, for logical organisation. ^ac448c
	- Also allows [[File Operations]] to be performed on groups of files

![[FileDescTable.png]]

- Each directory is managed via a *special file*
	- This contains a *file descriptor table*
		- Describes each file in the directory
			- Corresponding to entries in *global file table*

## Directory Structure

There are three types:
- [[Single-level (Flat) Directory Systems]]
- [[Two-level Directory Systems]]
- [[Hierarchical Directory Systems]]

### Implementation of Directories and Folders

- To open files, [[Pathing Methods|path names]] are used to locate a directory entry
	- This provides a *mapping* from a [[Naming Files|filename]]/[[File Attributes|file descriptor]] to the [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[File Systems#^a97394|blocks]] for a given file
		- Mapping varies depending on [[File Systems|filesystem]]:
			- [[Contiguous File Block Allocation|Contiguous allocation]] filesystems contain the addresses for the *entire file*
			- [[Linked-List File Block Allocation (Non-Contiguous)|Linked]] [[Linked List with File Allocation Table (FAT)|List]] allocation contain the *first* [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[File System]]