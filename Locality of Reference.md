# [Locality of Reference](https://en.wikipedia.org/wiki/Locality_of_reference)

This refers to the tendency for a CPU to access the same *locations* in memory repeatedly. As such, we try moving instructions/data *predicted* to be used from the bottom of the [[Memory Hierarchy]] to the top, so that CPU access times for these locations are as minimal as possible.