# Checklists and Fault Finding
## Fault Finding
There are two major methods of attempting to find faults; *scientific* - slow but sure - and *random* - if you're lucky. Somewhere between these extremes lies an *instinctive* method, based on unconscious knowledge of what symptoms link with which faults, built up by a sysadmin based on past experiences.

### The Scientific Method of Discovery
1) Examine the current situation, record it and record the fault(s) displayed.
2) Change *one* aspect of the situation and attempt to repeat the fault's circumstances.
	- Record the outcome.
3) Change this aspect back, and try again to verify the fault is repeatable under the same circumstances.
4) Repeat 2) and 3) with a different aspect each time, until sufficient evidence is built to draw a conclusion.
5) If a conclusion cannot be drawn, enumerate possibilities, and eliminate them one by one through changes to the system, via the same method outlined in 4).
6) When only one possible solution and cause is left, confirm it via an experiment. If that also fails to fix it, a possibility has not been enumerated.

#### Process of Elimination vs. Successive Refinement
##### Process of Elimination
Remove one part of a system at a time until the fault is resolved. The last part removed is the cause of the issue. Examples would include:
- Taking out memory chips until a machine can boot
- Removing conflicting drivers until an application can run/print.

##### Successive Refinement
Adding components to a system and verifying that the expected change occurs with each new installation. For example:
- Using logs in machines on the path of an e-mail to see its path from device-to-device.

### Further Clues to Consider
- *Has the situation EVER worked?*
	- If not, you're starting without information.
	- It is *has,* start by enumerating changes since last known working state.
		- Reliant on good records, however.

- *Can a user be trusted to give valid information?*
	- Sometimes users link unconnected items, insisting upon a relationship.

- *Are there multiple reports of this problem?*
	- If not, is it because reporting systems are inadequate, or because there really *is* a new problem?
		- If fault finding shows that it must have already existed, there are also faults in your reporting system.

### Gathering Information
*If a fault has been reported by a user:*
- Note the following:
	- User's name
	- ID
	- Location
	- Phone extension
- Find the ID of the desktop machine the fault occurred on.
- Find out the date/time of occurrence; it may not have just happened.
- Record what the user was trying to do, and the apparent symptoms:
	- Use open questions to gather details - "What were you expecting would happen?"
	- Find out why they were doing it - this leads to further information, as it may follow on from another problem.
- Get screen dumps if possible.
- Use remote login or other tools to get a list of software versions involved.
- File all of the above under a ticket number in a fault-reporting database, and assign priority (if allowed).

### Common Problems with Installing an OS
- *Failure to read a CD for install*
	- Connect an alternate supported drive.
	- Check CD for errors in another system.
- *Failure to install/start*
	- Is all hardware recognised by the OS?
- *Cannot connect to Domain Controller*
	- Is the *domain name* correct?
	- Are the DNS server and DC both online?
	- Is the NIC working and setup correctly?
	- Is there a computer account in the domain?
	- Has your account got rights to add computer accounts to the domain?

### Network Problem Tracing
![[Pasted image 20220321225242.png]]

- What does your machine *think* it is?
	- Use `ipconfig /all` to check the IP address.
- Can you ping the loopback address?
	- Ping `127.0.0.1` to check that TCP/IP is OK.
- Can you ping yourself?
	- If the host IP is correct in the table, this will forward packets to the loopback address.
- Can your PC connect anywhere?
	- Ping the default gateway to ensure it is working and that the PC can communicate with the local network.
- Can your PC see outside of the network?
	- Ping the IP of a remote host to see if you can get through the router to the Internet.
- Can your PC access DNS services?
	- Ping the hostname of a remote host to test that name resolution works.
- Is there any packet loss?
	- Use `pathping` to check for dropped packets that might indicate router failure.

### Printing Problems?
1) Make sure the printer is switched on, has paper and is connected directly to the print server, either directly or via network connection (i.e. by using `ping`)
2) Does the test page print?
	- Ensure that the print server has the correct driver and network address.
3) Does it print from other computers?
	- Ensure that this system is connected to the correct printer.
4) Does printing work for other users?
	- Check that the current user has valid permissions.
5) Is printing slow?
	- Print server may require more disk space, or defragging.

### Microsoft Device Driver Debugging
This assumes all causes outside the desktop PC itself have been eliminated, so you are left with either the application or an associated driver at fault.
- If the driver has recently been upgraded roll back to the previous version.
	- Else, try finding a more recent version using *System or Device Manager.*

Below is an image of the process undergone to manage a driver:

![[Pasted image 20220321225850.png

## Performance Tuning
![[Pasted image 20220321225938.png]]

Instantly, you should ask the following question: *Why?*
- Does the system perform adequately?
	- This depends on the stakeholder:
		- Users need performance.
		- Admins need system resources to be utilised efficiently.
- Can the system cope with changes in the period until the next upgrade?
	- If so, we *do not change.*

### Performance Problems
Initially, undergo the following protocol:
- Identify the source(s):
	- Use `perfmon`, *Task Manager,* etc.
	- Does the user complain about a particular application or accessing particular folders?
		- Some applications may have their own intensive needs, or a particular folder may be heavily accessed.
	- Is there a *baseline* to compare with?
		- Normally a single element in a chain will cause a bottleneck.
			- In these cases, upgrading other elements *will not help.*

#### Processors
There are a few metrics of processor performance:
- *Processor %time (desktop/server)*
	- If this is consistently above 85%, then a problem process may require identification and perhaps refactorization.
	- If a process *has* to run on this machine, then we need to upgrade or add a better processor.
- *Processor Queue Length*
	- This indicates how many program threads are waiting to run.
		- This should be < 2 threads/processor over an extended period; otherwise an upgrade is in order.
- *Processor % Interrupt time*
	- If > 15%, this may indicate faulty hardware that generates too many interrupts for the system to service.

#### Disks
There are also some metrics of poor disk performance:
- *Avg. Disk Sec/Read and Write*
	- If these exceed 25ms, the disk is causing the system to wait too long.
		- They should be under 10ms for critical apps such as SQL server.
		- Solution; *get faster disks.*
- *Avg. Disk Queue Length*
	- If $>(2\times \text{number of spindles})$, the physical disk system is a bottleneck.
- *Memory Cache Bytes*
	- If the space used for the filesystem cache is too large (300 MB), this can also indicate a disk bottleneck.

#### Memory
Memory problems can be due to leaks, insufficient ram, or `boot.ini` having /3GB switch (so insufficient kernel memory). Metrics include:
- *Available megabytes*
	- If $< 5\%$ of physical RAM, more is needed.
- *Pooling Non-Paged Bytes*
	- For objects that must remain in memory.
	- A possible memory leak can occur if greater than 175 MB, or 100 MB with a /3GB switch.
		- Event ID 2019 will be recorded in the system event log.
- *Pages/second*
	- Refers to the rate of reading pages from the disk to resolve hard page faults.
		- A value $> 1000$ is excessive, slows down the system, and may be a symptom of a memory leak.

#### Network
Problems in a network can be due to saturation or inadequate NIC performance - in which case, buy a faster card or segment the network. One metric is:
- *Bytes Total/Sec*
	- This is the rate sent/received over each adapter.
		- Should be $< 70\%$ of available bandwidth:
			- e.g. for a 100Mbps NIC, the limit is 8.7MB/sec:
				- $(100Mbps = 100000kbps = 12.5MB/sec)\times{70\%}$ 

#### Specific Applications
Some may have further diagnostics to assist us:
- Application log entries
- Own log files, dumped to disk.
	- Do you know *where,* though?
- They may provide additional counters to add to the performance monitoring system, such as:
	- Exchange
	- SQL Server