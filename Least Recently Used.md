# "Least Recently Used" Page Replacement

- Operates on the likelihood that *heavily used* pages *continue* to be used, and swaps out the pages left unused for the *longest time.*
	- Excellent performance!
	- Requires maintenance of a linked list of all *pages in memory*
		- Most recent at the head, least recent at the tail.
		- Must be updated with *every reference to memory*
			- Referenced page must be moved to the head.

Implementation is *difficult* and *time-consuming.*