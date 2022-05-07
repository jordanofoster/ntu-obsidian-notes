# Scheduling

- Schedulers decide which [[Processes|processes]] should be worked on next by the CPU.

- If current process *not* highest priority:
	1) **Save** process [[Processes#Process States|state]] in [[Processes#Process Tables|table]]
	2) **Retrieve** state of new highest-priori