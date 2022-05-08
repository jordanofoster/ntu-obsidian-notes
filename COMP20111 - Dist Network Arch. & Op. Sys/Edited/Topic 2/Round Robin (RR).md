#comp20111-dnaos/topic-2
# Round Robin (RR)

- Processes take turns using fixed *time quantum*
	- Typically ~10-20ms, lowers as clock increases
- Processes running overtime [[Interrupts|interrupted]], moved to back of queue
- **Heavy overhead** due to [[Scheduling#Context Switching|constant switching]].