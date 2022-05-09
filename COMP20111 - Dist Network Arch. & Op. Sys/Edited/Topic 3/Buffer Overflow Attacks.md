# [Buffer Overflow Attacks](https://en.wikipedia.org/wiki/Buffer_overflow)

These occur when a program writes data *outside* of the boundaries of the [[Memory Management#Address Spaces|address range]] it has been given, causing it to overwrite data in *adjacent* spaces. An example is shown below:

![[BufferOverflowAttk.png]]

1) `(a)` - Main program is running normally.
2) `(b)` - *Procedure* $A$ is called, asking for an address within `Main`'s *local variable* space.
3) `(c)` - A *buffer overflow* occurs, as `A`'s  *local variable* space now overlaps `Main`.

An example [C](https://en.wikipedia.org/wiki/C_(programming_language)) program that would cause a Buffer Overflow is as follows:
```
int position;
char buffer[2000];
position = 10000;
buffer[position] = 0;
```
