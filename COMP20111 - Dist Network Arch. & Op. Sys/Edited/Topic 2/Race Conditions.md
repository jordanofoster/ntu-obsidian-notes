## Race Condition

A *race condition* occurs when competition occurs on *resources* within *critical sections.* They are generally **unstable and undesirable.**

## Example 1 - Racing for Memory Access: 

A high-level program spawn threads `t1` and `t2`, that both manipulate the same variable, as shown below:

![[RaceConditionsExample1.png]]

We can break the program down into instructions, showing one possible [[Interleaving|interleaving]]:
1) `t1` retrieves `c`
2) `t2` retrieves `c`
3) `t1` increments `c`; result of `1`
4) `t2` increments c; result of `-1`

`t2` acted last upon `c`, and thus `t1`'s result is overwritten.

## Example 2 - Racing for Peripherals

Here, two [[Threads|threads]] are competing for access to the [[I/O|print spooler]] directory:

![[RaceConditonsExample2.jpg]]

Th