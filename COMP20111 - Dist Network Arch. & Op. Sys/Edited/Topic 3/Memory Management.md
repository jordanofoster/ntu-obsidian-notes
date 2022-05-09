# Memory Management

[[Processes]] share physical memory as well as CPU time. Instructions are fetched from [[Volatile Memory#Random Access Memory RAM|main memory]] and handed to the CPU for [[Fetch-Execute Cycle|execution]]; main memory is large enough to store *several* running processes at once.

![[MemMgmtDiagram.png]]

Therefore, we must use [[Memory Management]] for concurrent processes by taking advantage of [[Locality of Reference]] 