#comp20111-dnaos/topic-2
# Fetch-Execute Cycle

1) [[Processes|Process]] execution started by CPU
2) Fetch instruction from register
3) Execute instruction
4) Loop 2-3 until all instructions done
5) Terminate

If an [[Interrupts|interrupt]] is received from 2-3, [[Interrupts#Interrupt Handling|handle it]] and return.

![[FetchExecuteInterrupt.png]]