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

More seriously, though, the point of this strip i