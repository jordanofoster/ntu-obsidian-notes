#comp20111-dnaos/topic-2 
# Thread Interference

 An example has a high-level program spawn threads `t1` and `t2`, that both manipulate the same variable, as shown below:

![[RaceConditionsExample1.png]]

We can break the program down into instructions, showing one possible [[Interleaving|interleaving]]:
1) `t1` retrieves `c`
2) `t2` retrieves `c`
3) `t1` increments `c`; result of `1`
4) `t2` increments c; result of `-1`

`t2` acted last upon `c`, and thus `t1`'s result is overwritten.