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

Business intelligence refers to *a wide variety of tools, applications and methodologies that enable organizations to collect data from internal systems and external sources; prepare it for analysis; develop and run queri*