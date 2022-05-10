#comp20111-dnaos/topic-3 
# [[First Come, First Serve (FCFS) or First In, First Out (FIFO)|FIFO]] Page Replacement

A list of all [[Paging|pages]] currently stored in [[Volatile Memory#Random Access Memory RAM|main memory]] is maintained inside of itself. The most *recently arrived page* is at the list's tail; the *least recently* at the head. When required, the *head* page is removed, and incoming pages added to the *tail.* ^7b74db

The oldest page may still have use, and as such this method remains rarely used. ^0d4897