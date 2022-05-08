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
	- Executes in order of definition: $P \to Q \to R$

A sequential program can be represented in code (*High-Level*) or machine instructions (*System-Level*):

```
x = 1;		//P
y = x+1;	//Q
x = y+2;	//R

/* The final values of x and y depend on the order in which these statements are executed */
```

1) $P$ is a singular instruction:
	1) Store `1` at address of `x`
2) $Q$ is broken down into 3:
	1) Load value `x` into CPU register
	2) Increment register by `1`
	3) Store result at address of `y`
4) $R$ is broken down into 3:
	1) Load value `y` into CPU register
	2) Increment register by `2`
	3) Store result at address of `x`

