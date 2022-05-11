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