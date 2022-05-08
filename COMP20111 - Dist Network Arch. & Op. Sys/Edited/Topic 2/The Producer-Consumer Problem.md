# The Producer-Consumer Problem

This is a programming issue where a producer *produces* items, putting them in a buffer, and a *consumer* takes items *one-by-one* from that same buffer.

Some assumptions are made:
1) [[First Come, First Serve (FCFS) or First In, First Out (FIFO)|FIFO]] buffering is used
2) Producers can make new items at any time...
	- But the buffer **cannot be full**
3) Consumers can take items from the buffer...
	- But only if it **is not empty**
4) The program terminates when all produced items