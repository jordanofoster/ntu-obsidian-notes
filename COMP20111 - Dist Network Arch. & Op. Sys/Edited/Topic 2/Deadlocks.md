# Deadlocks

These occur when *two or more* [[Threads|threads]] are waiting upon each other. More accurately, four conditions must hold simultaneously:
1) **[[Inter-Process Synchronization#Mutual Exclusion|Mutual Exclusion]]** 
	- The resource is assigned to *one* [[Processes|process]] at a time.
1) **Hold and Wait** - [[Processes]] holding resources can request and wait for additional resources
2) **No preemption** - Previously-locked resources cannot be forcefully unlocked by another