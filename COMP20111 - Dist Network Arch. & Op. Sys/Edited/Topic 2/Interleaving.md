#comp20111-dnaos/topic-2 
# Interleaving

An *interleaving* is a *unique* sequence of [[Programs#Program Execution|statement executions]], in the context of several [[Concurrency|concurrent]] [[Threads|threads]] causing an unpredictable execution order. 

The number of possible interleavings for a for a set of processes can be calculated using:
$$\frac{(n_1 + n_2 + ... + n_i)!}{n_1!n_2!\times{...}\times{n_i!}}$$
where $n$ is the number of *[Atomic Instructions](https://stackoverflow.com/a/1762179)* in a [[Threads|thread]], and $i$ is the *number of threads* involved. This value increases *[exponentially](https://en.wikipedia.org/wiki/Exponential_function)* with *both* $n$ and $i$.

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