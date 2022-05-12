# System Monitoring

## What is system monitoring?

System monitoring software analyses the operation and performance of the system. It can also intervene in operation and performance. System monitoring is used in a few situations:

**No intervention**
- Only system logs are taken.

**Alerts**
- The system detects and alerts about possible errors and/or unusual behaviour.

**Emergency Management**
- Shuts down the system if extreme levels are reached

**Everyday Management**
- Automatically changes system parameters to optimise performance.

### Why monitor systems?

System monitoring improves the use of hardware; by detecting poorly functioning machines, they are fixed faster. Incidents themselves are also detected faster, and sometimes prevented.

The faster resolution of problems improves customer service and organizational reputation, as less human hours are required to manage systems.

#### What should be monitored?

**Servers:**
- Availability/uptime
- Performance
- Resources
- Errors
- Event logs
- Databases
- Security

**Employees:**
- Log all applications used
- Time spent on different projects
	- For project management purposes
- Email usage
	- Maybe with alerts for certain content/attachments
- File sharing
	- With same alerts as for emails
- Use of personal email/communications
	- Especially if company data is being attached
	- Or even use keyword searching for conversations about the boss
- Social media usage

**Other Users:**
- E.g. contractors, visitors, customers, students
- Log applications used
- Log logins, attempted and actual
- Log use of removable media, such as USB drives
	- And files transferred in both directions
- Log/have alerts on file sharing and attachments

**Websites:**
- Load times
	- For first byte, for the page to be ready
- Redirect, DNS and connect duration
- Back-end send & receive duration
- Front-end Document Object Model & rendering duration
- Monitoring can be passive
	- "Real user" monitoring can be used, where we wait for someone to view the page
- Or active:
	- Synthetic monitoring, involving loading the page regularly
- This is not neccessary for static websites, but not many of these still exist.

#### How to monitor

##### Business Intelligence

![[Pasted image 20211206194326.png]]

Business intelligence refers to *a wide variety of tools, applications and methodologies that enable organizations to collect data from internal systems and external sources; prepare it for analysis; develop and run queries against that data; and create reports, dashboards and data visualizations to make the analytical results available to corporate decision-makers*

###### Is it really intelligent?

Information is data, combined and applied; Knowledge is information, combined and applied. Wisdom is applying the right knowledge at the right time. As a result, Business Intelligence really refers to *Information Management* - but the use of the word intelligence underlies the selection of information to display.

###### Primary Business Intelligence Tool: Dashboards

Dashboards are graphical user interfaces that provide views on key performance indicators. These vary depending on the organisation's goals, but should aim for the following:

- Should be quantifiable
- Should indicate performance in some way
- Performance should be linked to organisation's objectives

An example of a dashboard is as follows, using a school in South Wales:

*"We used to be 6 weeks behind the curve when it came to analysing issues and finding patterns. Now, everything is tracked instantly via the dashboard."*

*"High attendance is very important to us, and every day our attendance officer looks at the first morning registrations via the dashboard and immediately starts ringing homes to find out what is wrong and where the absent children are."*

*"She also looks at attendance per lesson. As an example, if someone is absent from a mid-morning French class who was registered at the start of the school day, she will personally intervene and get them back to class."*

![[Pasted image 20211206194847.png]]

###### Key features of Business Intelligence tools
- Visual data discovery
- Ease of use for non-IT users
- Self-service (user-designed without needing specialist BI/IT teams)
- Integrates with common data formats (spreadsheets, databases, etc)
- Local database more popular than cloud
- Data mining/analysis
	- Business Intelligence is not just the dashboard itself

###### Market Overview

![[Pasted image 20211206195058.png]]

###### Microsoft BI tools

[There are plenty to choose from,](https://hub.packtpub.com/what-bi-and-what-are-bi-tools-microsoft-dynamics-gp/) such as:

- Excel Power Query, which combines data from various sources, including Wikipedia and some other websites:
- Power BI:
	- Upload data (e.g. Excel table) into dashboard
	- Ask questions in natural language
	- See results visually, as a graph, chart, table or map
	- pin common queries to the dashboard
- Power Map:

![[Pasted image 20211206195455.png]]

##### Good Practices

- The priority is communication, not looking good.
	- Horizontal bar charts are preferred, as the human eye is trained to read across a page
- Put key information above the 'fold' and to the left
	- Fold being the point where users have to scroll down to see it.
		- This may be different on a mobile app.
	- Left vs right is again due to order of reading.
- Context and exceptions:
	- Don't just display figures such as '76%' - how good or bad is it?
	- Allow users to set up expectations and alerts that appear when certain values are reached.
- Be sparing with colour.
- Integration and sharing are vital:
	- Web-based tools are preferred, and it must be easy to share key results with other tools/users 

##### Bad practices

- Make the IT department the sole leader of the dashboard implementation
- Choose measurements that do not depict the organisation's objectives
- Choose inappropriate visual objects
- High ink-to-data ratio
	- Microsoft PowerMap?
- Over-crowding visual objects on a single screen
- Overuse of visual effects, colours and decorations
- Unappealing UI design
- Deployment of the dashboard without incorporating it in management routines