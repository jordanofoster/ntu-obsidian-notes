# Virtual Memory

This is a [[Memory Management]] technique allows the *partial* storage of [[processes|processes]] on [[Non-Volatile Memory#Hard Drives|secondary storage]] to be loaded to [[Volatile Memory#Random Access Memory RAM|main memory]] when required, through [[Memory Management#Memory Abstraction|abstraction of storage]] already available on the machine - done by presenting a large 'pool' of memory to developers/users that hides [[Swapping]] and the [[Memory Hierarchy]].

## Interplay between Virtual Memory and Swapping

[[Swapping]] allows several [[Processes|processes]] to run where the **sum of their sizes** is greater than total *available* [[Volatile Memory#Random Access Memory RAM|RAM]]. [[Virtual Memory]] allows [[Processes|processes]] **larger** than our *total* [[Volatile Memory#Random Access Memory RAM|RAM]] size to run - and is implemented using [[Paging]] and [[Segmentation]].
