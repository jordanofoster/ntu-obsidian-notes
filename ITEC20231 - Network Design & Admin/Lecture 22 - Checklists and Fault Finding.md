# Checklists and Fault Finding
## Fault Finding
There are two major methods of attempting to find faults; *scientific* - slow but sure - and *random* - if you're lucky. Somewhere between these extremes lies an *instinctive* method, based on unconscious knowledge of what symptoms link with which faults, built up by a sysadmin based on past experiences.

### The Scientific Method of Discovery
1) Examine the current situation, record it and record the fault(s) displayed.
2) Change *one* aspect of the situation and attempt to repeat the fault's circumstances.
	- Record the outcome.
3) Change this aspect back, and try again to verify the fault is repeatable under the same circumstances.
4) Repeat 2) and 3) with a different aspect each time, until sufficient evidence is built to draw a conclusion.
5) If a conclusion cannot be drawn, enumerate possibilities, and eliminate them one by one through changes to the system, via the same method outlined in 4).
6) When only one possible solution and cause is left, confirm it via an experiment. If that also fails to fix it, a possibility has not been enumerated.

#### Process of Elimination vs. Successive Refinement
##### Process of Elimination
Remove one part of a system at a time until the fault is resolved. The last part removed is the cause of the issue. Examples would include:
- Taking out memory chips until a machine can boot
- Removing conflicting drivers until an application can run/print.

##### Successive Refinement
Adding components to a system and verifying that the expected change occurs with each new installation. For example:
- Using logs in machines on the path of an e-mail to see its path from device-to-device.

#### Further Clues to Consider
- *Has the situation EVER worked?*
	- If not, you're starting without information.
	- It is *has,* start by enumerating changes since last known working state.
		- Reliant on 