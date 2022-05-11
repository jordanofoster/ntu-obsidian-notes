#comp20111-dnaos/topic-4 
# File Structure

Files can be structured in one of three ways:
- [[File Structure#Byte Sequence|Byte Sequence]]
- [[File Structure#Record Sequence|Record Sequence]]
- [[File Structure#Tree|Tree]]

## Byte Sequence

- OS inherently considers files *unstructured*
	- Has [[Programs|programs]] interpret byte sequences themselves
		- Used by Windows/UNIX
	
## Record Sequence

- Treats files as *sequence* of *fixed-length*, *structured* records:
	- Collection of bytes:
		- Mainly used when *punch cards* still in use

![[RecordSequence.png]]

## Tree

- Each *variable-length* record has a *key field*
	- used for *record retrieval*
		- Useful in *databases*

![[TreeSequence.png]]