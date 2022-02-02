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

Now *ListCommand* is visible within the *myLibrary* namespace, and the class can be accessed as `myLibrary.ListCommand`.

### Interfaces

An interface allows the definition of a specific interface to a class; any class that implements it will have to provide a set of pre-defined method signatures. Interfaces cannot include implementation, private, protected or internal members. All of them should be *public.*

```
namespace myLibrary
{
	public Interface MyListInterface
	{
		void add(object onj);
		object get(int index);
		int size();
		void toString();
	}
}
```

### *this* and *is* keywords

*this* refers to the current instance of an object:

```
private string name;
public void setName(string name) {
	this.name = name;
}
```

*is* provides the user with a way to determine if the object supports an interface. If it does, then methods within the interface can be accessed. Syntax is `<expression> is <type>`.

```
Employee CKent = new Employee("Clark Kent");
if( CKent is Employee ) CKent.print();
```

### Control Structures

C# provides the same control structures as C/C++ and Java, such as the *if* statement:

```
if( x == 10) {
	// ...
} else {
	// ...
}
```
Remember that when comparing objects, `if( obj == obj2 ){}` does not compare that the two object *contain the same data,* but instead comparing the pointers of each object. Strings are different in this regard, however:

```
String name1 = "clark";
String name2 = "lois";
if( name1 == name2 ) Console.WriteLine("they are the same!");
else Console.WriteLine("they are not the same!")
```

Additionally, the switch statement:

```
switch( value ) {
	case 1:
		Console.WriteLine("Option 1!");
		break;
	case 2:
		Console.WriteLine("Option 2!");
		break;
	default:
		Console.WriteLine("Option 2!");
		break;
}
```

### Loops

For loops are the same as in C#/Java:
```
for (int iCounter = 0; iCounter < 10; iCounter++)
{
	Console.WriteLine("counter = " + iCounter);
}
```

For each:
```
List<string> myList = new List<string>();
for (int counter = 0; counter < 10; counter++) {
	myList.Add("item " + counter);
}
foreach (string value in myList) {
	Console.WriteLine(value);
}
```

### Reading/Writing to console

```
namespace ConsoleApplication1
{
	class Program
	{
		static void Main(string[] args)
		{
			Console.WriteLine("Enter first mumber: ");
			int value1 = Convert.ToInt32(Console.ReadLine());
			Console.WriteLine("Enter second number: ");
			int value2 = Convert.ToInt32(Console.ReadLine());
			Console.WriteLine("multiplying {0} by {1} gives {2}",
								value1, value2, (value1 * value2));
		}
	}
}
```

### Exception Handling

C# provides the user with *throw* and *try-catch* statements so that you can handle unwanted exceptions. Classes that can be used within C# code will usually throw an exception if an error occurs, especially if you are relying on 3rd-party APIs and libraries:

![[Pasted image 20220118003934.png]]
![[Pasted image 20220118004039.png]]
[A final link.](https://insecure.org/stf/smashstack.html)

## C\# Implementations

### Inheritance:

![[Pasted image 20220124162737.png]]

### Interfaces

![[Pasted image 20220124162802.png]]

### Properties

In C\#, properties can be used to access private data. This is done by using the *get* and *set*
methods to allow read and write access respectively.

![[Pasted image 20220124163003.png]]

#### Why Properties?

- Making the class field *Public* and exposing it to the external world is not a good programming practice, as you will not have control over what gets assigned and returned.

![[Pasted image 20220124162901.png]]


#### Get and Set methods

![[Pasted image 20220124163122.png]]

#### Override

![[Pasted image 20220124163152.png]]

### Handling data (Arrays)

Arrays are fixed-length collections of homogenous objects. For example, you can have an array of integer data types, Employee objects, etc.

In C\#, Arrays are firstly class objects; this means they must be initialised with the `new` keyword

```
int arrayOfInt[256]; // Wrong!
int arrayOfInt[] = new int[256]; // creating an array of 256 integers
```

C\# has a shortcut for creating array objects and initialising them where the `new` is not required:

```
int smallPrimes = {2, 3, 5, 7, 11};
```

#### Array Initialisation Methods

Arrays can also be multi-dimensional:

```
// 2-dimensional array
int[,] array1 = new int[10, 10];
// using a for loop to initialise values
for (int i = 0; i < 10; i++)
{
	for (int j = 0; j < 10; j++)
	{
		array1[i, j] = 0;
	}
}
```

```
// could also initialise array this way...
int[,] array2 = { { 1, 1 }, { 2, 2 }, { 3, 3} };
```

### Methods and Parameter Passing

![[Pasted image 20220124163655.png]]


## A quick note on Access Modifiers

![[Pasted image 20220202005630.png]]

## What is a Cmdlet?

Cmdlets are specialised .NET classes that implement a specific tasks or operation, such as an executable file. Cmdlets have required and optional parameters that control how they operate, and are named using a *verb-noun* pairing; the verbs are used to describe what actions the cmdlet will perform, and nouns are used to describe what entity the cmdlet will perform the action on.

### Cmdlet naming

- Verbs are action-oriented words e.g.:
	- Add
	- Get
	- Set
	- Update
- Nouns describe what command to act on e.g.:
	- SPSite
	- SPUser

Note that all nouns for SharePoint begin with SP; there are 893 cmdlets alone on SP server 2019.

Examples encountered in NDA labs include:

- New-ADComputer
- Get-Help
- Set-ADUser
- Get-Spsite
- Get-PSSnapin
- New-SPContentDatabase

There are lots of pre-defined verbs, stored in classes:
- VerbsCommon
- VerbsCommunciations
- VerbsData
- VerbsDiagnostic
- VerbsLifeCyle
- VerbsSecurity
- VerbsOther

### Sending input to cmdlets

Cmdlets can accept parameters:

```
new-gpo -name "Publishers Policy"
```

Cmdlets can also be chained together so that the output of one can be input to another:

```
new-gpo -name "Publishers Policy" | new-gplink -target "ou=publishers, dc=testnetwork, dc=com"
```

Here, `new-gpo` is creating a new GPO object and passing it (using the pipe symbol `|`) to the `new-gplink` cmdlet. The `new-gplink` cmdlet links a GPO to a site, domain, or organizational unit (OU).

### Anatomy of a cmdlet

![[Pasted image 20220202010354.png]]

### Processing within cmdlets

The Cmdlet and PSCmdlet classes provide the following methods:
- `BeginProcessing()` - Provides a one-time, pre-processing functionality for the cmdlet.
- `ProcessRecord()` - Provides a record-by-record processing functionality for the cmdlet.
- `EndProcessing()` - Provides a one-time, post-processing functionality for the cmdlet.

These methods need to be implemented by the developer; sending objects through a pipeline between cmdlets can then be demonstrated by the following:

![[Pasted image 20220202010600.png]]

Each of the methods is inherited from the PSCmdlet class so we need to use the `protected` and `override` modifiers.

```
protected override void EndProcessing()
{
	base.EndProcessing();
}

protected override void BeginProcessing()
{
	base.BeginProcessing();
}

protected override void ProcessRecord()
{

	foreach (string name in nameCollection)
	{
		WriteVerbose("Creating salutation for " + name);
		string salutation = "Hello, " + name;
		WriteObject(salutation);
	}
}
```

## Snap-ins

Once you have finished writing your C\# cmdlet, you have to create another file which contains snap-in information. Snap-ins are used to register cmdlets with PowerShell, and to setup any registry entries. If you do not register a cmdlet within PowerShell, you will not be able to run it; A snap-in for the cmdlet would be added to your project and linked in when the project is compiled.

### Anatomy of a Snap-in

![[Pasted image 20220202011000.png]]

### Snap-ins vs Module

Snap-ins include not only PowerShell commands, but also other supporting .DLLS or applications that you might need in order to get snap-in or commands within that same snap-in to work.

Modules are another way that PowerShell commands are packaged; it is a preferred packaging technique and is demonstrated in later sections.

### Compiling cmdlets and linking into PowerShell

1) Cmdlets can be created and compiled within Visual Studio.
	- You need a special template project to create cmdlets; they can be downloaded from the web.
2) Cmdlets can also be compiled using the .NET framework's C\# compiler, `csc.exe`.
	- It is found under `windows\Microsoft.Net\Framework\<.net version>`
3) Use the `installutil` command to register the cmdlet in PowerShell.
4) Use `add-pssnapin <new cmdlet>` to access the cmdlet from a PowerShell prompt.

## PowerShell Scripting

PowerShell provides a rich scripting language that is used to provide more complex functionality by linking cmdlets together. There are various types of languge features available:

- Variables
- If/else statements
- Switch statements
- For loops
- Command line parameter passing

and so on.

### PowerShell Scripting Example

```
[int] $intPing=10
[string] $intNetwork="127.0.0."

for($i=1; $i -le $intPing; $i++) {
	$strQuery = "select * from win32_pingstatus
  where address = ' " + $intNetwork + $i + " ' "
	$wmi = get-wmiobject -query $strQuery
	"Pinging $intNetwork$i ..."
	if( $wmi.statuscode -eq 0 )
		{"success"}
	else
		{"error: " + $wmi.statuscode + " occurred"}
}
```

Variables have the following syntax:

`[<data type]$<variable name> = <data value>`

The following data types are available:
- `[array]`
- `[char]`
- `[decimal]`
- `[hashtable]`
- `[long]`
- `[single]`
- `[bool]`
- `[byte]`
- `[double]`
- `[int]`
- `[string]`
- `[xml]`

If statement syntax is as follows:

```
if( $<variable name> <evaluation expression> <value> )
	{"success"}
else
	{"fail"}
```

Comparators in PowerShell scripting are as follows:

- `-eq` is equal to $(=)$
- `-lt` is less than $(<)$
- `-gt` is greater than $(>)$
- `-ge` is greater than or equal to $(\geq)$
- `-le` is less than or equal to $(\leq)$
- `ne` is not equal to $(\neq)$

### PowerShell Switch example

Switch statement syntax is as follows:

```
switch <expression evaluation type> ($<variable name>) {
... expressions ...
}
```

a few examples are shown below:

```
[int] $simpleSwitchExample = 2

switch ($simpleSwitchExample) {
	1 { "Option 1" }
	2 { "Option 2" }
	3 { "Option 3" }
	default { "No idea..." }
}
```

```
[string] $regularExpressionSwitchExample = "1234"
[int] $size = 0

switch -regex ($regularExpressionSwitchExample) {
	"\d{4}" { $size = 4; break; }
	"\d{3}" { $size = 3; break; }
	"\d{2}" { $size = 2; break; }
	"\d{1}" { $size = 1; break; }
	default {
		"No idea..."
		$size = -1
		}
}

if( $size -gt 0 ) { "The string had " + $size + " characters " }
else { "Wasn't able to work out how many characters!" }
```

In the second example, `-regex` refers to a regular expression. Simiarly, `-wildcard` refers to wildcard matching

### Getting input from the user

Scripts can interact with the user to provide more functionality; for example, they can display information by just saying - for example - "message..." However, this is not formatted.

We can use the `Write-Host` cmdlet to display output instead, and we can format the message (colours, spaces, etc.) To provide an example:

`Write-host "hello world" -foregroundcolor black -backgroundcolor white`

Scripts can get input from the user by using the `Read-Host` cmdlet. For example:

`$ipAddress = Read-Host "Enter the ip address:"`

Additionally, the `-AsSecureString` option to mask what has been entered:

`$password = read-host -assecurestring "Enter your password:"`

### PowerShell Functions

```
function display {
	param ([string]$message="")
	Write-Host "Your message is $message"
}

display "hello world"
```

```
function display( $message ) { % Un-typed 
	Write-Host "Your message is $message"
}

display "hello world"
```