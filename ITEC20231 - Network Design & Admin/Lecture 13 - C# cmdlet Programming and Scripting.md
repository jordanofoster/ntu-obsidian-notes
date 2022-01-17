# C\# cmdlet Programming and Scripting

## Why do  sysadmins need to know about programming?

There are many reasons:

- Tools are not available to perform the task for you, so we have to write new tools
- Scripting provides more power than executing single command line tools
- Automation of tasks
- Alteration of OS, especially if Unix based

## Powershell

![[Pasted image 20220117234540.png]]

Powershell is referred to as the *next generation command shell and scripting language.* It provides access to a lot of powershell programs, known as cmdlets. Cmdlets can be joined together, by piping the output of one to the input of the other, and powershell provides a set of scripting commands to facilitate this. Cmdlets can be programmed to do specific tasks as well.

[This link provides more info.](https://programming.oreilly.com/2013/06/powershell-command-line-introduction.html)

### What knowledge is needed to program a cmdlet?

Mainly, C#; this is a C++/Java-esque language that requires the .NET framework to be installed. Cmdlets are written in C#, but the following is also required:

- Extension of the ***PSCmdLet*** class
- Providing parameter attributes
- Implement the following methods:
	- **BeginProcessing**
	- **ProcessRecord**
	- **EndProcessing**

Then, provide your code. [](https://msdn.microsoft.com/en-us/library/zw4w595w.aspx)