# Messaging Systems

## Single vs Multiple Systems

When writing an application, it tends to be written as a single program running on a single computer. However, this approach does not work when a program is scaled to run over multiple systems. 7

As such, we need to consider how the problem can be solved by distributing functionality across multiple programs, running on multiple nodes.  We also have to consider how to access this functionality remotely, in the form of a method or object. There are a number of approaches, and they are mainly categorised as direct or indirect:

![[Pasted image 20220221131317.png]]
![[Pasted image 20220221131321.png]]
![[Pasted image 20220221131329.png]]

## Local Procedure Calls

Java programs require methods to be written to call other methods. This procedure is called *local procedrure calling*. An example of such is shown below:

```
Receiver receive = new Receiver(destinationPort);
Sender send = new Sender(3000, destinationPort);

receive.start();
send.start();
```
