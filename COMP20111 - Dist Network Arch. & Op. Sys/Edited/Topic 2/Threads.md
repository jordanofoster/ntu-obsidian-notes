# Threads

Threads are *independent* execution paths/sequences within a [[Processes|process]].
 
- Parts of *some* processes can be *parallelised* for efficiency/usability
	- This is known as *multithreading*
		- Generally improves application performance

New threads are stored in a [[Processes#Process Tables|Thread Control Block (TCB)]] upon creation. They share other similarities with processes:
- [[Processes#^49d2fc|Flow of Control]]
- Single [[Processes#^26a0a7|Point of Execution]]
- [[Processes#Process States|States]]
- [[Scheduling#Context Switching|Context Switching]]
- [[Spawning+Forking|Spawning/Forking]]

But differences too:
- Only existent *within* a [[Processes|process]]
	- [[Spawning+Forking|created/controlled]] by an existing process
- Share [[Address spaces|propertie]]
