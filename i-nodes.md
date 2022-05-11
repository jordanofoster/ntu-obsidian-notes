#comp20111-dnaos/topic-4 
# i-nodes

- Used by UNIX and derivatives
- Each file associated with *i-node* (index node) ^d5818b
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
- 3 *indirect pointers* exist ^a70acb
	- Point to further [[Memory Management#Logical Address Spaces|address]] blocks
		- Eventually leads to another disk data block
	- First pointer is a *single level* of indirections ^04578a
		- Next is a *double indirect pointer* ^628e47
			- Third a *triple indirect pointer*

### Example of File Location with [[i-nodes#i-nodes in UNIX|UNIX i-nodes]]

Given [[Pathing Methods#^5ccc9c|absolute path name]] `/usr/ast/mbox`:

1) System locates *root [[Directories and Folders|directory]]'s [[i-nodes#^d5818b|i-node]]*
	- [[i-nodes#^a70acb|second]] *i-node* **always has a fixed position**
		- [[i-nodes#^04578a|first]] *i-node* is **reserved**
			- Used to store/track *bad blocks* on disk to prevent use by other files
2) First path component (`usr`) looked up, to find *i-node* number of that file/directory
3) With `/usr`'s *i-node number*, i-node data accessed to find [[i-nodes#^628e47|next]] nu