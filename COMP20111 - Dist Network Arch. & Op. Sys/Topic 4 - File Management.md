# File Management

## Current Position (Windows)

![[Lecture4CurrentPos.png]]

### Why non-volatile storage?

It is desirable that the data we store can persist for both later use and further processing, and this should happen even after power-down or unpredicted shutdown (critical errors, crashes or otherwise forced terminations).

RAM is insufficient for this purpose as  information in the process address space is lost with the process' termination - its limited capacity also makes it far too small to be able to handle all data at once for most applications.

### Files 

Files are uniform logical units of information that are created by a process. They also have address space - but this is mapped to a mass-storage unit rather than RAM itself. Put simply, they are named collections of related information recorded on secondary storage, such as the lines of code in a program or a set of words in a text document.

Files are used to store large amounts of data in the long-term, and several processes may be allowed to access the file data concurrently, as seen below:

![[Files.png]]

#### Naming of Files

The motivation behind this is so that the user does not have to use numerical addresses to refer to specific files, instead going by a user-friendly human-language title. Different OSes enforce different naming conventions, but most follow a common pattern; many for example support up to approximately 260 characters for names, such as Windows/Unix.

![[Pasted image 20211115164740.png]]

There are also generally restrictions on characters that can be used; for example `?` can't be used in Windows, but this is valid in Unix. Case sensitivity is also noted amongst OSes - Unix is, whereas Windows is not.

![[Pasted image 20211115165116.png]]

**File extensions** are useful to tell both OS and user what type of data a file contains:
- In MS-DOS, only 3 characters were allowed for extensions
- In unix, the amount of characters used is up to the user.

UNIX itself as an OS does not enforce file extensions; rather, software used in it enforce them instead (such as a C compiler needing a `.c` file extension to compile with).

OSes more associated with GUIs tend to attatch meanings to extensions by associating applications to them, such as using Microsoft Word to open a `.docx` file. This presents a security issue, as it is easy to trick/corrupt files by modifying extensions. To prevent this, MacOS instead attempts to examine the file and determine its type by looking at its contents.

An example table of commonly used file extensions and their meanings is shown below:

| Extension | Meaning |
| --------- | ------- |
| `file.bak` | Backup file |
| `file.c` | C source program |
| `file.gif` | Graphical Interchange Format image |
| `file.html` | Word Wide Web HyperText Markup Language document |
| `file.iso` | ISO image of a CD-ROM (for burning to CD) |
| `file.jpg` | Still picture encoded with the JPEG standard |
| `file.mp3` | Music encoded in MPEG layer 3 audio format |
| `file.o` | Object file (compiler output, not yet linked) |
| `file.pdf` | Portable Document Format file |
| `file.ps` | PostScript file |
| `file.tex` | Input for the TEX formatting program |
| `file.txt` | General text file |
| `file.zip` | Compressed archive |



#### File Structure

Files can be structured in one of three ways:

###### Byte Sequence

With this method, the OS inherently considers files as unstructured, leaving it up to the program that accesses one to interpret the byte sequence itself. This method is used by both Windows and Unix.

###### Record Sequence

![[Pasted image 20211115165823.png]]

This treats files as a sequence of fixed-length, structured records - a collection of bytes, mainly useful when punch cards were still commonplace.

###### Tree

![[Pasted image 20211115165829.png]]

Each variable-length record has a key field, used for record retrieval. Useful in database systems.

#### File Types

Most OSes support several types of files:
- **Regular:** ordinary files that contain data
- **Executables:** contain program code that can be executed by the OS.
- **Directory/folder:** System files containing references to other file types.
- **Character special:** Not true files, but directories that refer to character devices.
	- This allows communication with I/O devices such as printers.
- **Block special:** Again, not true files, but directory entries which refer to block devices.
	- Used for communication with storage devices, such as disks or main memory.

![[Pasted image 20211115170142.png]]
Example layout of an executable file.

![[Pasted image 20211115170146.png]]
Example layout of an archival file.

##### File Attributes

A table of example file attributes is shown below:

| Attribute | Meaning |
| --------- | ------- |
| Protection | Who can access the file and in what way |
| Password | Password needed to access the file |
| Creator | ID of the person who created the file |
| Owner | Current owner |
| Read-only flag | `0` for read/write; `1` for read only |
| Hidden flag | `0` for normal; `1` for do not display in listings |
| System flag | `0` for normal files; `1` for system files |
| Archive flag | `0` for has been backed up; `1` for needs to be backed up |
| ASCII/binary flag | `0` for ASCII file; `1` for binary file |
| Random access flag | `0` for sequential access only; `1` for random access |
| Temporary flag | `0` for normal; `1` for delete file on process exit |
| Lock flags | `0` for unlocked; non-zero for locked |
| Record length | Number of bytes in a record |
| Key position | Offset of the key within each record |
| Key length | Number of bytes in the key field |

#### Typical File Operations

Operating Systems offer several system calls for file management:

- **Create**  - The file is created with no data. Some attributes are associated with it.
- **Delete** - The file is deleted to free up disk space.
- **Open** - Before using a file, a process must open it to fetch attributes/disk addresses into RAM.
- **Close** - When all accesses are finished; attributes/disk addresses that have been loaded are no longer needed.
- **Seek** - Used for random access files. repositions file pointer to specific location in file.
- **Get attribtutes** - Retrieves the attributes for the file (e.g. useful for C compilers).
- **Set attributes** - Some attributes can be user-set, such as protection-mode.
- **Rename** - Change the name of an existing file.
- **Read** - Data is read from file.
- **Write** - Data written to existing file.
- **Append** - Restricted variant of write. Can add data only to the end of the file.

#### File Access

![[Pasted image 20211115172856.png]]

File access refers to the way in which files stored may be accessed, [[Topic 3 - Memory Management#Abstraction|as discussed in topic 3.]] There are two types:

- **Sequential Access**
	- Still interesting today due to the *locality principle*
		- Read next, Write next
- **Random (or direct) access**
	- Random access is essential for most applications.
		- Where $n =$ relative block number:
			- Read $n$
			- Write $n$

### Directories/Folders

Most filing systems allow files to be grouped in directories or folders, resulting in more logical organisation. This allows operations to be performed in bulk on groups of files, such as copying files or setting their attributes - as well as allowing different files to have the *same filename* so long as they are in *different directories.*

![[Pasted image 20211115173543.png]]

Each directory is managed via a special file, which contains a *file descriptor table* with descriptors for each file under that directory, corresponding to specific entries on the global file table.

#### Directory Structure

There are three types of systems for each directory structure:
- **Single-level (flat)**
- **Two-level**
- **Hierarchical**

##### Single-level (Flat) Directory Systems

![[Pasted image 20211115174007.png]]

One directory is used for all files in the volume (e.g. four files are owned by 3 different people, `A`, `B`, and `C`). This structure was mainly used in early mainframes, being very simple and allowing the ability to quickly find files - but it also struggles from naming and grouping problems as a result of its design.

##### Two-level Directory Systems

![[Pasted image 20211115174121.png]]

A separate directory is used for each user, with letters dictating owners of directories and files. It has the benefit of allowing the same file name for different users, but at the cost of limited grouping capability.

##### Hierarchical Directory Systems

![[Pasted image 20211115174446.png]]

These are directories that present themselves in a tree-like structure; this method grants grouping capabilities and [[Topic 4 - File Management#Directories Folders|allows the same file name for files in different directories]] - but this is at the cost of requiring a method to browse/locate files (such as `ls, cd, pwd` for Unix).

#### Paths

![[Pasted image 20211115174815.png]]

Two common pathing methods are used to browse files:
- **Absolute path name** - which is relative to the route directory and unique:
	- `/` in UNIX -> `/NTU/dnaos/demo.c`
	- `\` in MS-DOS/Windows ->  `\NTU\dnaos\demo.c`
- **Relative path name** - relative to the current/present working directory, for example:
	- If current directory is `/NTU/dnaos/`, then a file whose absolute path is `/NTU/dnaos/demo.c` can be referred to simple as `demo.c`.
	
Special entries such as `.` and `..` can be used too:
- `.` -> *current directory*
- `..` -> *parent directory*
	- e.g. `cd .`, `cd ..`

#### Directory Operations

OSes provide the following system calls for directories:

- **Create** - an empty directory is created
- **Delete** - an existing directory can be deleted (empty or non-empty?)
- **Opendir** - directories can be read e.g. to list all files in a directory
- **Closedir** - when directories are read, they should be closed to free up space.
- **Readdir** - next entry in open directory
- **Rename** - same method as files
- **Link** - technique that allows files to appear in more than one directory
- **Unlink** - If a file is unlinked, it is typically only present in one directory normally.

More directory specific syscalls exist depending on OS used.

#### File Systems Layout

![[Pasted image 20211115175505.png]]

Drives are divided into partitions/volumes, each holding an independent file system. Section 0 is the **master boot record (MBR)** - this is used to boot the computer via a **boot block** from a specified partition, from which the OS is loaded.

The **super block** contains info about the partition (e.g. the number of blocks).

##### File Block Allocation Methods
Blocks are subdivisions of mass storage originally related to disks. They are very much similar to both [[Topic 3 - Memory Management#Paging|pages and their frames, used in main memory.]]

![[Pasted image 20211115180914.png]]

The objective of file block allocation is to keep track of which files go to which block on a physical drive. There are different schemes to achieve this:

- **[[Topic 4 - File Management#Contiguous Allocation|Contiguous allocation]]** (used in CDs)
- **[[Topic 4 - File Management#Linked List Allocation (Non-Contiguous)|Linked list allocation]]** - non-contiguous
- **[[Topic 4 - File Management#Linked List with File Allocation table|Linked list with file allocation table]]** (used in DOS/Windows)
- **[[Topic 4 - File Management#Allocation with i-nodes|i-nodes]]** ([[Topic 4 - File Management#i-nodes in Unix|used in UNIX]])

###### Contiguous Allocation

![[Pasted image 20211115181405.png]]

Contiguous allocation is a simple implementation, only needing to store the first block address and its length - thereby being very performant, allowing ease of random access, and providing robustness against drive faults, as damage to a single block only causes localised loss of data.

However, the size of files when initially created must be tracked, and files themselves cannot grow; for example an existing document cannot be edited by introducing new data.

Fragmentation occurs as files are deleted and holes left in their place; as with main memory, this can be overcome with [[Topic 3 - Memory Management#Compaction|compaction]] but comes with the same downsides.

###### Linked List Allocation (Non-Contiguous)

![[Pasted image 20211115182154.png]]

Files in this method are stored as *linked lists of blocks.* The first bytes of each block are used as a pointer - and each block contains both its own data and a pointer to the next block, with the final block containing a *null* pointer.

This has some major advantages; every block is usable, file sizes don't need to be known beforehand and thus can grow, and there is no risk of external or internal fragmentation (with the exception of the last block for the latter).

However random access is not supported as this method is very slow due to the chain of blocks requiring traversal, and the pointers required for each block causes a slight data overhead.

###### Linked List with File Allocation table

![[Pasted image 20211115182551.png]]

This method is used by older versions of MS-DOS/Windows, and proposes a major improvement over basic linked list allocation by introducing a *file allocation table* (FAT) that stores all pointers in memory. This was standardised in different ways, causing different filesystems such as FAT16 and FAT32.

The FAT must be in memory at all times - to get a file, we simply point to the location inside of it that contains the memory address of the first block.

This has the clear advantage of freeing up space that would otherwise have been occupied by block-specific pointers, and as the pointers are stored in faster main memory, random access is much quicker - and drive references aren't required either.

However the FAT may get too large - especially for physical drives with higher capacities. Damage to the FAT may also cause serious data loss, though this can be mitigated by storing several backups of it.

###### Allocation with i-nodes

![[Pasted image 20211115182842.png]]

These are used by UNIX-type OSes. Each file is associated with an i-node (index-node) that lists all file attributes and the drive/disk addresses of each block associated with the file. With this, all blocks corresponding to the file can be found easily.

This has the advantage of only requiring the i-node of a file to be in memory, and only when the file corresponding to an i-node is opened; but if files grow beyond the limits of an i-node, the last disk-address listed must point to an address block instead of a data block, causing excess overhead.

###### i-nodes in Unix

I-nodes in unix contain a number of **direct** pointers to disk blocks, typically of which there are 10. 

![[Pasted image 20211115183043.png]]

In addition to this, 3 **indirect** pointers exist, which point to further address blocks that eventually lead to another disk data block. The first of these pointers is a **single** level of indirections, with the next being a **double** indirect pointer, and the third a **triple** indirect pointer.

##### Shared Files

File Systems also allow the sharing of files at different points within the file hierarchy, as shown below:

![[Pasted image 20211115183253.png]]

#### Implementation of Directories/Folders

To open files, a path name is used to locate its directory entry. This directory entry then provides a mapping from a filename/file descriptor to the disk blocks that contain the data.

![[Pasted image 20211115173543.png]]

This directory entry contains all the information needed to find the disk blocks for a given file, dependent on filesystem:

- **Contiguous allocation** filesystems contain addresses of the entire file.
- **Linked list allocation** filesystems merely contain the first disk block address.
- **i-node implementations** contain the directory's i-node number.

The directory entry also allows access to the file's attributes; the structure of which differs based on operating system, as the diagram below shows, using DOS as figure `a` and UNIX as figure `b`:

![[Pasted image 20211115183743.png]]

To be more exact, in DOS, a directory entry contains the attributes itself:

![[Pasted image 20211115183808.png]]

Whereas in UNIX, each directory entry has an i-node number and filename. All of the directory's attributes are stored in the i-node, and all i-nodes have fixed locations on the disk - meaning locating one is simple and fast.

![[Pasted image 20211115183848.png]]

##### Example of Locating A File in UNIX

Given an absolute path name of `/usr/ast/mbox`:
1. The system locates the root directory's i-node.
	- i-node 2 **always has a fixed position** as i-node 1 is **reserved** and used to store/keep track of bad blocks on the disk to prevent use by other files.
2. Next, the first path component (`usr`) is looked up in the root directory, to find the i-node number of *that* file
3. With the i-node number for `/usr`, the i-node data is accessed to find the next i-node number for `usr/ast`
4. This process is repeated until the actual file (in this case `mbox`) is located.

Accessing relative path names are identical, with the exception that the search starts from the current working directory.

![[Pasted image 20211115184349.png]]

After `/usr/ast/mbox` is located, the i-node of `mbox` is held in memory until the file is closed. Locating files in other hierarchical file systems is similar i.e. by looking things up component by component.

### Determining Block Size

All allocation methods require the disk be split into fixed-size blocks, and almost all modern systems use blocks as such. The trade-off is similar to [[Topic 3 - Memory Management#Comparison of Paging Segmentation|page size in memory management:]]

- With small block sizes, a file may occupy several blocks. This causes longer access time since more blocks have to be located, and thus a greater overhead.
- With larger block sizes, small files such as 1KB will occupy a big chunk of the disk block (e.g. 32KB), causing wasted space.

As a result, typical block sizes are used, such as 512B/1KB/2KB.

### Tracking Free Space

Much like with [[Topic 3 - Memory Management#Managing Free Space|main memory]], both linked lists and bitmaps are options:

#### Linked List Method

![[Pasted image 20211115185051.png]]

Some of the free blocks left over are used to hold free disk block numbers. These blocks are linked together, making their own linked list of free blocks that can be written to.

#### Bitmap method

![[Pasted image 20211115185221.png]]

Bitmaps are stored with one bit per block that records whether it is free or not; `1` is free, `0` is used. As a result, bitmaps occupy less space than linked lists - 1 bit per block instead of the 32 bits required by the latter.

However, the number of blocks required to track free space in a bitmap is *constant* - the number of blocks required to track free space in a *linked list* becomes *less as the drive fills.*

#### Consistency

File systems read, modify and write blocks - meaning that if they crash before all modifications have been written out, errors can occur; this is known as *Inconsistency.* An example diagram showing file system states is shown below:

![[Pasted image 20211115185754.png]]

`a`: Consistent.
`b`: Missing block.
`c`: Duplicate block in free list.
`d`: Duplicate data block.

Most OSes offer utility programs in order to deal with this; UNIX has `fsck` and Windows has `chkdsk`.


##### Journaling

Single file operations may actually require multiple writes to disk. Using UNIX as an example when removing a file:

1. Remove file from its directory
2. Release the i-node to the pool of free i-nodes
3. Return all disk blocks to pool of free blocks

Analogous steps are required in Windows.

Issues can occur in event of error; if the first task above completes and then the system crashes, the i-node and file blocks will not be accessible from any file, or be available for reassignment. Fixing this requires time-consuming repairs, such as `scandisk` etc.

![[Pasted image 20211115190302.png]]

*Journaling* file systems use a special area of the disk to make a log entry listing actions that need to be completed. In the event of failure, the log is used to bring the disk back into a consistent state (i.e. by completing all pending actions). Log entries are erased once operations complete successfully.

### RAID (Redundant Array of Inexpensive Disks)
`Learnt about more in Network Design & Administration`

Disks, excluding SSDs, remain a bottleneck in computer systems. RAID aims to mitigate this by distributing data across several physical disks, which look like a singular logical disk. This adds another layer of abstraction.

Using many disks in parallel provides many benefits to performance and reliability, depending on implementation:

- RAID 0 (striping) distributes data across several disks, in a way which improves speed and gives full capacity. However it has **no security whatsoever.**
- RAID 1 (mirroring) uses more than one disk to store the same data. This degrades speed and doesn't ensure full capacity, but the security of data is ensured.
- RAID 1+0 takes advantage of both:

![[Pasted image 20211115190825.png]]

### Security in File Systems

`This topic is touched upon more in both NDA and Cyber-Security.`

Access to file can be done through Access Control Lists, where each object (e.g. file) contains a list of principals that list what can be done to the object:

![[Pasted image 20211115191836.png]]

### Minix File System Layout - Implementation Example

![[Pasted image 20211115191916.png]]

Above is the disk layout for a small hard-disk partition containing 64 i-nodes and a 1KB block size (i.e. two consecutive 512B sectors are treated as a single block).

![[Pasted image 20211115192149.png]]

The API and procedures for both block and i-node management are shown below:

| Procedure | Function |
| --------- | -------- |
| `get_block` | Fetch a block for reading or writing |
| `put_block` | Return a block previously requested with `get_block` |
| `alloc_zone` | Allocate a new zone (to make a file longer) |
| `free_zone` | Release a zone (when a file is removed) |
| `rw_block` | Transfer a block between disk and cache |
| `invalidate` | Purge all the cache blocks for some device |
| `flushall` | Flush all dirty blocks for one device |
| `rw_scattered` | Read or write scattered data from or to a device |
| `rm_lru` | Remove a block from its LRU chain |

Procedures used to manage the superblock and bitmaps are also shown below:

| Procedure | Function |
| --------- | -------- |
| `alloc_bit` | Allocate a bit from the zone or i-node map |
| `free_bit` | Free a bit in the zone or i-node map |
| `get_super` | Search the superblock table for a device |
| `get_block_size` | Find a block size to use |
| `mounted` | Report whether given i-node is on a mounted (or root) filesystem |
| `read_super` | Read a superblock |


### Distributed File Systems

`Looked at again in term 2/3`

It has been shown in this topic, that an OS and PC will have a filesystem. In distributed systems, we must consider many separate machines with their own file systems. How is this space managed

![[Pasted image 20211115193034.png]]