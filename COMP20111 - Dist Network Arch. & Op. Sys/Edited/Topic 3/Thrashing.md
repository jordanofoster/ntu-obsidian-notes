# [Thrashing](https://en.wikipedia.org/wiki/Thrashing_(computer_science))

Thrashing occurs when the CPU spends *more time [[Swapping|swapping]] [[Paging|pages]]* and [[Paging#Page Fault Handling|handling page faults]] than *[[Programs#Program Execution|executing]] the [[Processes|processes]] they hold*. It is typically a sign that [[Virtual Memory]] is overloaded - and that we have loaded *too many processes.* 

According to the related Wikipedia article, Thrashing *"causes [machine performance] to degrade or collapse"* - and can *"continue indefinitely"* until the issue is resolved, either by the user or the OS.