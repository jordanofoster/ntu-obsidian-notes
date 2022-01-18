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
![[Pasted image 20220117235135.png]]

Mainly, C#; this is a C++/Java-esque language that requires the .NET framework to be installed. Cmdlets are written in C#, but the following is also required:

- Extension of the ***PSCmdLet*** class
- Providing parameter attributes
- Implement the following methods:
	- **BeginProcessing**
	- **ProcessRecord**
	- **EndProcessing**

Then, provide your code. [Another link.](https://msdn.microsoft.com/en-us/library/zw4w595w.aspx)

## C# vs. Java
### Data Types
C# has the same primitive data types as seen in C++ and Java;

`int` (e.g. `int value = 5;`)
`bool` (e.g. `bool receivedInput = false;`)
`float` (e.g. `float value = 8.5;`)
`arrays` (e.g. `string []params;`)	

C# does however have more complex data types:
- String
- List
- ArrayList
- Stack
- Queue
- ...

### Classes

In C#, everything is an *Object.* A class provides the blueprint as to what data and operations can be offered. However, you have to use the class blueprint to create an object instance before it can be accessed. C# class syntax is similar to Java otherwise, however;

```
public class MyFirstClass {
	public MyFirstClass() {
		// Constructor ...
	}
}
```

![[Pasted image 20220117235730.png]]

### Anatomy of a C# Program

![[Pasted image 20220118000200.png]]

### Strings

Strings are objects of the **System.String** class. A sequence of characters can be assigned to them using the assignment operator $=$ , as shown below:
`String machineName = "MAE108-34";`

Strings can also be joined together using the $+$ operator:
`String fullName = machineName + ".ads.ntu.ac.uk"`

Because *String* is a class, it comes with several useful methods and properties, including *Length* (returns number of characters in string) and *Substring(`int startPosition, int length`)* which returns characters between two 'bound' characters, such as `start` and `start+length`.

### Inheritance

C# allows functionality to be inherited from another class:
![[Pasted image 20220118000615.png]]
![[Pasted image 20220118000629.png]]

#### Concept of Inheritance

![[Pasted image 20220118000649.png]]

![[Pasted image 20220118000655.png]]

### Namespaces

C# provides the user with hundreds of usable classes for use in programs. Each class created will have a name, as seen below:

`public class ListCommand`

However, what happens if another class called *ListCommand* exists? In this case, Namespaces can be used to limit the scope of any defined classes:

```
namespace myLibrary
{
	public class ListCommand
	{
		// ...
	}
}
```

Now *ListCommand* is visible within the *myLibrary* namespace, and the class be 