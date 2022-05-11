#comp20111-dnaos/topic-5 
# [[Interrupts|Interrupt]] Handlers

![[Pasted image 20211206161953.png]]

- [[Interrupts]] are important in the I/O stack
	- Not trivial to handle - several steps required:
		1) Save registers *not* already saved by hardware
		2) Set up context for [[Interrupt Service Routine (ISR)s|ISR]]
		3) Set up *stack* for [[Interrupt Service Routine (ISR)s|ISR]]
		4) Acknowledge *interrupt controller*
		5) Copy registers from where they were saved to the [[Processes#Process Tables|process table]]
		6) Run [[Interrupt Service Routine (ISR)s|ISR]] to extract information from *device control registers*
		7) Choose which [[Processes|process]] is run next
		8) Set up [[Memory Management Unit (MMU)|MMU]] context for [[Processes|process]] to run next
		9) Load new [[Processes|process']] registers
		10) Start running new [[Processes|process]]