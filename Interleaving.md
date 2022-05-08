# Interleaving

An *interleaving* is a *unique* sequence of [[Programs#Program Execution|statement executions]], in the context of several [[Concurrency|concurrent]] [[Threads|threads]] causing an unpredictable execution order. 

An example shows 10 different [[Threads|threads]], causing 10 interleavings:

![[Interleaving.png]]
One run of a program corresponds to *one* interleaving sequence, which determines a unique order of statement execution.

## Example using code

Using `t1` and `t2` as an example:
```
t1;
begin s1; ... sm; end;

t2;
begin p1; ...; pn; end;

begin t1, t2;
end;
```