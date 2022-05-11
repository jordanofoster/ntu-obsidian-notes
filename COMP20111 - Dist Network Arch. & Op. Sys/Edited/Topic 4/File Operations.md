#comp20111-dnaos/topic-4 
# File Operations

These are syscalls related to file management, provided by the OS. Some examples include:

- **Create**
	- File is created with *no data.*
		- Some attributes are associated.
- **Delete**
	- File is deleted to free [[Non-Volatile Memory#Why use Non-Volatile Storage comp20111-dnaos topic-4|disk space]].
- **Open**
	- [[Processes]] must *open* files to fetch attributes/[[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[Memory Management#Logical Address Spaces|addresses]] into [[Volatile Memory#Random Access Memory RAM|RAM]].
- **Close**
	- Used when all access is finished and loaded attributes/addresses are *no longer needed.*
- **Seek**
	- Used for *Random Access* files. Repositions file pointer to specific location in file.
- **Get Attributes**
	- Retrieve file attributes. Useful for some programs.
- **Set attribute**
	- Self-explanatory. Some can be user-set, such as protection-mode.
- **Rename** ^ac5401
	- Change file name.
- **Read**
	- Read data from file.
- **Write** ^6d560d
	- Write data to *existing* file.
- **Append** ^558d90
	- Restricted variant of [[File Operations#^6d560d|write]] - can add data only to *the end* of a file.