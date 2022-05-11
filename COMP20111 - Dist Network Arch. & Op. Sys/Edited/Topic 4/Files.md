#comp20111-dnaos/topic-4 
# Files

- Named collections of *related information* put on [[Non-Volatile Memory|secondary storage]] 
	- In uniform [[Memory Management#Logical Address Spaces|logical units]]
	- Created by [[Processes|processes]]
	- Have their own [[Memory Management#Logical Address Spaces|address space]]...
		- ...but mapped to [[Non-Volatile Memory#Why use Non-Volatile Storage comp20111-dnaos topic-4|mass storage]] instead of [[Volatile Memory#Random Access Memory RAM|RAM]]
- Stores large amounts of data in the long-term
	- [[Processes]] can access file data concurrently:
		>![[Files.png]]

## Naming Files

- Done so that user doesn't need *numerical addresses*
	- Different OSs enforce different filename conventions
		- Some common patterns:
			- $\text{char length} \leq 260$ - Windows/UNIX
			- Character restrictions:
				- `?` invalid in Windows, valid in UNIX
			- Case sensitivity:
				- UNIX is
				- Windows isn't

 ![[FileBasenameExtension.png]]

- **Extensions** tell OS/user the *type* of data stored:
	- For MS-DOS, no longer than 3 characters
	- UNIX doesn't care (user choice)
		- Doesn't enforce extensions itself
			- Programs do instead - e.g. C compiler wants `.c` files
- OSs with GUIs associate *app*