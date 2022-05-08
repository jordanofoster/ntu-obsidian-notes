# Threads

- Threads are *independent* execution paths/sequences within a [[Processes|process]] 
	- Each process has *one* execution thread by default.
 
- Parts of *some* processes can be *parallelised* for efficiency/usability
	- This is known as *multithreading*
		- Generally improves application performance

New threads are stored in a [[Processes#Process Tables|Thread Control Block (TCB)]] upon creation. They share other similarities with processes:
- [[Processes#^49d2fc|Flow of Control]]
- Single [[Processes#^26a0a7|Point of Control]]
- [[Processes#Process States|States]]
- [[Scheduling#Context Switching|Context Switching]] 
