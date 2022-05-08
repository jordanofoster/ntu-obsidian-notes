# Interleaving

This refers to the issue of several [[Concurrency|concurrent]] [[Threads|threads]] causing an unpredictable execution order. An example shows 10 different instances, yielding 10 possible unique sequences:

![[Interleaving.png]]
One run of a program corresponds to *one* interleaving sequence, which determines a unique order of statement execution.

## Example using code

