#comp20111-dnaos/topic-2
# Highest Response Ratio Next (HRRN)

*Derived* from [[Shortest Job First (SJF)]] - attempts to *reduce long job starvation*
- Jobs assigned [[Scheduling#Prioritization Metrics|priorities]] based on:
	- [[Memory]]
	- [[Time]]
	- Other requirements
		- $(\text{waiting time} + \text{run time}) / \text{run time}$
- **Highest** priority (*Response Ratio*) first
- Priorities change when *new jobs added*