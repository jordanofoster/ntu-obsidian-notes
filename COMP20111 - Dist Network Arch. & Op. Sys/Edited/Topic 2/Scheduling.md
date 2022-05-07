# Scheduling

- Schedulers decide which [[Processes|processes]] should be worked on next by the CPU.
- Changes made via a *[[Scheduling#Context Switch|context switch]]*

## Context Switch

- If current process *not* highest priority:
	1) **Save** process [[Processes#Process States|state]] in [[Processes#Process Tables|table]]
	2) **Retrieve** state of new highest-priority process
	3) Begin/Resume process, as indicated by program counter.

- **Causes overhead** - should be minimized.