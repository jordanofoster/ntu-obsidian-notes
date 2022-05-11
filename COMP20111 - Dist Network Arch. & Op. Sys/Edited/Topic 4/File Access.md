#comp20111-dnaos/topic-4 
# File Access

![[FileAccessTypes.png]]

File access refers to how we access stored files, as a form of [[Memory Management#Memory Abstraction|abstraction]]. There are two types:

- **Sequential Access**
	- Still interesting today due to [[Locality of Reference]]
		- Reads/Writes *next*
- **Random/Direct Access** ^174f37
	- Essential for most applications!
		- Where $n = \text{relative block number}$
			- Read $n$
			- Write $n$ 