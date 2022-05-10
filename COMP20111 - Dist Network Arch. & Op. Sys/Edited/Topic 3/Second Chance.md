# "Second Chance" Page Replacement

This is a [[FIFO Page Replacement|FIFO]] variant that avoids accidentally replacing an [[FIFO Page Replacement#^0d4897|old page]] that may be *heavily used*, by checking its [[Paging#^bec2a7|reference]] bit first:

![[SecondChancePgReplacement.png]]

If unset (`0`), it is replaced; otherwise, it is cleared and moved to the [[FIFO Page Replacement#^7b74db|tail]] of the page - thereby *resetting* load-time. It then continues onto the next page:

![[SecondChancePgReplacement2.png]]

This still unnecessarily moves pages, but improves on [[FIFO Page Replacement|FIFO]] regardless.