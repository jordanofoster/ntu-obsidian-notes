#comp20111-dnaos/topic-5 
# [[Interrupts|Interrupt]] Handlers

- [[Interrupts]] are important in the I/O stack
	- Not trivial to handle - several steps required:
		1) Save registers *not* already saved by hardware
		2) Set up context for [[Interrupt Service Routine (ISR)s|ISR]] 