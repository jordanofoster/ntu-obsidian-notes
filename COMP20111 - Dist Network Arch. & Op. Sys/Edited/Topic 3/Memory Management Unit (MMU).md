# Memory Management Unit (MMU)

MMUs map [[Memory Management#Memory Abstraction|logical]] addresses to [[Memory Management#Referencing Physical Memory|physical]] addresses, using registers to map partition locations.

## Base and Limit Registers

![[BaseLimitRegs.png]]

- Base Registers store the *starting address* of a *logical partition.* 
	- Limit Registers store their *length.*

When *logical* addresses are referenced, the Base Register performs the following:
1) Check to see if it is within the *partition range specified*
2) *[[Memory Management Unit (MMU)#^615611|Relocate]]* any references to the actual *physical* address.

## Memory Protection & Relocation

- The value of the *Base Register* is added to the *logical* address, mapping to a *physical* address. This process is known as *Relocation.* ^615611
	- Logical addresses greater than the *Limit Register* are *invalid.* This acts as a form of *Memory Protection.*

The *address* component of a machine instruction acts as an offset for the *base* address. To demonstrate:

> ![[MemProcReloc.png]]

1) Base address is `101`.
2) Instruction is `JMP 5`.
3) $101 + 5 = 106 
   - $\therefore$ *logical* `JMP 5` $\rightarrow$ *physical* `JMP 106` 