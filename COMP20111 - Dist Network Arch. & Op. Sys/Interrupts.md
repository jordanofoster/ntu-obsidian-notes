# Interrupts
- Signals sent to CPU
- Require **immediate attention**

## Interrupt Handling

Using an [[Processes#^1436ce|I/O event]] as an example:

1) Event occurs. Process execution **suspended.**
2) CPU begins work on **another process.**
3) Process goes from **[[Processes#^1436ce|BLOCKED]]** to **[[Processes#^555d69|RUNNING]]** 