# Multi-Level Feedback Queues (MFQ)

Technically *not* a scheduling algorithm:
- Consists of several queues using *other algorithms*
- Each queue prioritised differently
- Used to *maintain common processes*
	- e.g. I/O in one queue, CPU in another
- Jobs can *move queues* when [[Scheduling#Prioritization Metrics|priority]] changes