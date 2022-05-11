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