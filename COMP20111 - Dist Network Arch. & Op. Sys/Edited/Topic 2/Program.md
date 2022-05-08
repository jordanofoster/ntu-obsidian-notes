#comp20111-dnaos/topic-2
# Program

- A program *is compiled binary* of source-code.
- Several [[Processes|processes]] can be derived from the same program.
- Programs can be written [[Programming#Sequential Programming|sequentially]] or [[Programming#Concurrent Programming|concurrently.]] 

## Program Execution

When a process is executed, a [[Processes|process]] is created. This is considered the 'main [[Threads|thread]]' of the application.

### Sequential Program Execution

There is only ever *one possible execution sequence.* For example:

- A program with statements $P, Q, R$:
	- Executes in order of definition: $P -> Q \arrow R$
