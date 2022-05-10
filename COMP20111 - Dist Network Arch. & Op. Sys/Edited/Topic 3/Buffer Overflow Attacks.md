#comp20111-dnaos/topic-3 
# [Buffer Overflow Attacks](https://en.wikipedia.org/wiki/Buffer_overflow)

These occur when a program writes data *outside* of the boundaries of the [[Memory Management#Address Spaces|address range]] it has been given, causing it to overwrite data in *adjacent* spaces. An example is shown below:

![[BufferOverflowAttk.png]]

1) `(a)` - Main program is running normally.
2) `(b)` - *Procedure* $A$ is called, asking for an address within `Main`'s *local variable* space.
3) `(c)` - A *buffer overflow* occurs, as `A`'s  *local variable* space now overlaps `Main`.

An example [C](https://en.wikipedia.org/wiki/C_(programming_language)) program that would cause a Buffer Overflow is as follows:
```
int position;
char buffer[2000]; //Our buffer is 2000 bytes long
position = 10000; //Position is byte 10,000
buffer[position] = 0; //We try to write to byte 10,000 - outside buffer!
```

In modern systems, various [[Memory Management Unit (MMU)#^4c942c|memory protection]] measures prevent this, but it still occurs in the wild - for example in [homebrew](https://en.wikipedia.org/wiki/Homebrew_(video_games)) communities, as seen with [NTRCardHax](https://courses.csail.mit.edu/6.857/2019/project/20-Chau-Ko-Tang.pdf) on the Nintendo 3DS.