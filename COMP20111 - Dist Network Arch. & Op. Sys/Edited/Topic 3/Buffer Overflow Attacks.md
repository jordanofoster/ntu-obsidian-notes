# [Buffer Overflow Attacks](https://en.wikipedia.org/wiki/Buffer_overflow)

These occur when a program writes data *outside* of the boundaries of the [[Memory Management#Address Spaces|address range]] it has been given, causing it to overwrite data in *adjacent* spaces. An example is shown below:

![[BufferOverflowAttk.png]]

1) `(a)` - Main program is running normally.
2) `(b)` - *Procedure* $A$ is called