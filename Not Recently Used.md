# "Not Frequently Used" Page Replacement

This method uses [[Paging#^bec2a7|reference]] and [[Paging#^621b28|modified]] bits in the [[Paging#Page Tables|page table]] to collect usage statistics on pages, like so:

- Class 0, `0 0` -> Not referenced/Not modified
- Class 1, `0 1` -> Not referenced/Modified
- Class 2, `1 0` -> Referenced/Not Modified
- Class 3, `1 1` -> Referenced/Modified

[[Paging|Pages]] from the *lowest-numbered, non-empty* class are removed; [[Interrupts#^46cbff|a timer interrupt]] clears the [[Paging#^bec2a7|reference]] bit, distinguishing between pages *recently* referenced, and those not. It has *very low* overhead and *easy implementation*, but is *not optimal.*