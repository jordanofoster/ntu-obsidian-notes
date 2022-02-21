# Malicious Intent

The assumption is made that any organisation or individual with computers is a target for malicious intent, and that some attackers will be specifically targeting you, whereas others will just see you as a resource to exploit (targeted vs. dragnet attacks).

Methods of attack can be many and varied, as can attackers. Specific threats will be discussed only in as much as there are specific strategies to counter them. The security in practice module (year 3) will go into exploiting and defending against attacks.

## Dangers in Security

Concentration on a few known threats can leave targets vulnerable to those unconsidered. Targeting specific vectors is not enough, and an overall security programme has to be devised. Security itself may have to be handled by a sysadmin already overloaded with day-to-day tasks. They may be tempted to either lock everything down, or allow easy access to avoid hassle.

### Types of security concerns

There are a number of security concerns a sysadmin has to be aware of, such as:
- Coding errors (some):
	- Buffer overflows
	- Trapdoors (not an error, but someone adding extra code to circumvent security)
- Attacks (some):
	- SQL Injection
	- Dictionary Attacks
	- DDOS attacks
- Viruses
- Rootkits
- Spyware/Malware

The question is what sysadmins can do to help protect against these.

#### Example of a 'false target'

- [The top 25 types of coding errors](http://cwe.mitre.org/top25/)
- [A full CWE list of 1000+ problems](http://cwe.mitre.org/data/index.html)
	- This includes eveything from SQL injection (CWE-89) to improper access control (CWE-285).
	- 'Errors' here range in scale from coding bugs, to an overall failure to architect security structure.
	- As a result, it may tempt managers to concentrate *only* on those indicated issues.
		- Many of these errors are moreso symptoms of a bigger problem, such as sloppy coding standards, inadequate testing regime or a lack of managerial control.

See [Software \[In\]security: Top 11 Reasons Why Top 10 \(or Top 25\) Lists Don't Work](http://www.informit.com/articles/article.aspx?p=1322398)

#### SQL Injections
[As explained by xkcd.]([xkcd: Exploits of a Mom](https://xkcd.com/327/))

More seriously, though, the point of this comic strip is that any application may be considered vulnerable, unless proven otherwise. Microsoft has been quoted as saying that ["Perfect Security is Impossible".](http://msdn.microsoft.com/en-us/library/ft0y04t6(vs.71).aspx) A holistic approach must therefore be taken.

#### Command Injection

The code below shows how a simple Python program for copying a file to another destination can introduce a potential exploit:

```
import os
systemCommand = "cp"
srcFile = input("Please enter the name of the source: ")
dstFile = input("Please enter the name of the destination: ")
systemCommand += srcFile + " " dstFile
os.system(systemCommand)
```

Calling `os.system` will get the OS to execute the command given. This can be a problem:
- `"readme.txt + readme2.txt"` is fine.
- `"readme.txt readme2.txt;" + "rm -rf/"` is not!
	- This copies the file and then recursively deletes all files on the filesystem.
		- Sure, access control/authorisation can help reduce this; but what if SU/root did this?
			- Files would be deleted until the system was broken so much that it could not even do that!

#### Buffer Overflows

![[Pasted image 20220221165050.png]]

The above images show the following:
- (a) is a situation when the main program is running.
- (b) shows the situation after procedure A is called.
- (c) shows a buffer overflow in grey.

(For additional investigation; Stack Smashing, Metasploit, and [other penetration tools](https://sectools.org))

#### Trapdoors
```
# (a): Normal code with no security exploits

def login():
	name = password = ""
	while True:
		name = input("Login:")
		password = input("Password:")
		v = check_validity( name, password )
		if v:
			break
	execute_shell(name)

# (b): Code with a trapdoor inserted

def login():
	name = password = ""
	while True:
		name = input("Login:")
		password = input("Password:")
		v = check_validity( name, password )
		if v or (name == "clarkkent"): # Trapdoor
			break
	execute_shell(name)
```

for `(b)`, we can see that when checking whether the username and password is valid (stored in `v`) the next line introduces a trapdoor to see if the result is a valid set of credentials, *or* if the username is the same as `"clarkkent"` - this would circumvent our password security check!

#### [Dictionary Attacks](http://www.sci-tech-today.com/news/Data-Breach-Offers-Lessons-for-CIOs/story.xhtml?story_id=13300EUMKOJ4)

```
Set WinHttpReq = CreateObject("WinHttp.WinHttpRequest.5.1")
WinHttpReq.Open "POST", "http://www.domain.com/login", false
WinHttpReq.SetRequestHeader "Content-Type","application/x-www-form-urlencoded"
WinHttpReq.Send("login=Chris&password=Pa$$w0rd")
```

Dictionary attacks are a form of brute-force attack; we connect to a server many times a second, and send dicti