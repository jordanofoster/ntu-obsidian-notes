#comp20111-dnaos/topic-3 
# Clock Page Replacement

Much like [[FIFO Page Replacement|FIFO]], but with pages on a *circular* list:

![[ClkPgReplacement.png]]

Avoids unnecessary page movement, unlike [[FIFO Page Replacement|FIFO]] and [[Second Chance]]. The hand points towards the *oldest* page, checking its [[Paging#^bec2a7|reference]] bit without actually moving it.