#comp20111-dnaos/topic-4 
# i-nodes

- Used by UNIX and derivatives
- Each file associated with *i-node* (index node)
	- Lists all [[File Attributes|file attributes]] and [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[Memory Management#Logical Address Spaces|addresses]] of each block associated with file
		- All blocks corresponding to file can be found easily
- Only requires *i-node* to be in memory
	- and *only* when corresponding file opened
- Files can grow beyond *i-node* limits
	-  Last [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[Memory Management#Logical Address Spaces|address]] listed *must point* to *address block* instead of *data block*
		- Causes *excess overhead*

## i-nodes in UNIX

![[UnixINodes.png]]

- Contain a number of *direct pointers* to [[File Systems#^a97394|disk blocks]]
	- Typically 10 of these
- 3 *indirect pointers* exist
	- Point to further [[Memory Management#Logical Address Spaces|address]] blocks
		- Eventually leads to another disk data block
	- First pointer is a *single level* of indirections
		- Next is a *double indirect pointer*
			- Third a *triple indirect pointer*

