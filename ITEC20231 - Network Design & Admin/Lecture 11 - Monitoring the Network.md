# Monitoring the Network

## Monitoring vs. Accessing

Administrators have great power over the network, so they must use it judiciously:
- Changing permissions, changing ownership, etc.
	- Allows them to silently example drives on remote machines while users still logged on
- Additionally, can monitor actions, resource usage and processes.

Admins are very busy however and do not have time to watch everything.

## Historical vs. Real-time monitoring
*Historical* monitoring summarises information over a time period. This is essential for organizations trying to understand and improve their own performance, as it indicates a need for upgrades and justifies spending.

*Real-time* monitoring looks at current/recent situations, in order to understand problems/issues. This method typically generates relatively quick actions/responses.

### Monitoring User Machines

Monitoring typically implies high-level, light-touch procedures, such as:
- How much is a user printing?
- How close is a user to their disk quota?

Detailed management checking is also implied:
- What are users actually storing on-disk?
- How active are users on their computers?

Monitoring can also be needed for security, to detect indicators, such as a large amount of failed login attempts at one particular machine.

### Monitoring Servers

We monitor servers because they are a mission critical resource to an organization, and as such we need to catch potential problems before they cause delays/inconvenience, and thus costs. Problems may include:

- Running out of disk space/disk faults
- Memory leaks due to faulty programs
- Network limitations
- Dead services/daemons meaning tasks not performed
- General resource shortages

### How to monitor/check machines

There are numerous methods:
- Using the *Microsoft Management Console* locally.
- Physically logging on at the user machine.
- Remote logins.
- Using MMC to access *other* machines.
- Using logs/audit trails/real-time monitoring.

One factor that affects which method is used is budget (e.g. cost of sending technicians directly to user stations vs. remote logins).

#### Microsoft Management Console

![[Pasted image 20211210161704.png]]
![[Pasted image 20211210161708.png]]

This has already been encountered when looking at users and computers, but the MMC provides a central point of management for different objects and resources. It can be started via one of two methods; via *admin tools*, or using *mmc.exe* and including a snap-in (such as *gpedit.msc*).

The MMC can also be redirected to another machine.

#### Physically logging in

This can obviously be inconvenient to both user and admin, but it is sometimes necessary, such as when a network card has failed.

More frequently, this is done when helping a particular user, as they prefer local presence - although the cost of doing so is high.

#### Remote Log in

This is *much* cheaper than physically accessing a device, and generally acts as a better solution.

This is achieved through the use of Remote Desktop to log into a client machine; the software is also particularly used for monitoring servers, which may be in remote locations.

*Remote Desktop* uses Remote Desktop Services at the target machine, and a client program, known as *Remote Desktop Connection*, at the admin's machine.

Alternatively, remote administration can be done via PowerShell, with the use of `ssh` required on Unix machines.

It should be noted that setup is required at both ends for remote login to be possible.

##### Client-side remote desktop access

![[Pasted image 20211210162246.png]]

Clients can simply set-up access from the system properties. By default, the *Administrator* group are granted remote access permission, though additional users can also be added.

##### Remote Desktop Services/Virtual Desktop Infrastructure

This was previously called *Terminal Services* in *Windows Server* versions before 2008, and allows clients to use a server as if it were their own PC.

###### Configuring server-side remote desktop services

![[Pasted image 20211210162455.png]]

##### Remotely accessing a Unix server

Naturally, not all servers run windows; a number of organizations use Unix/Linux within their workplace. These machines may be setup to provide various roles, such as:

- DNS
- Web Server
- File Server
- Print Server

(In summary, basically everything Windows Server can do).

### Monitoring the Server

As stated before, the health of a server needs to be constantly monitored due to their importance within organizations. Things that are monitored include:
- Processor usage/temperature
- Disk performance/usage/throughput
- Memory utilisation
	- Page files, etc.
- Network parameters

When monitoring servers, the best practice is to start from a baseline; although this may change over time as new hardware and software is added.

#### Monitoring via the Event Viewer

![[Pasted image 20211210162903.png]]

This is accessible via the *Administration Tools* menu, and should be looked at regularly, as part of a procedure. The event viewer can also access event logs on a remote machine.

##### Event Logs

- Application:
	- About specific programs
		- Depends on what is logged by developers
- System:
	- About components.
		- Driver failure, service failure, etc.
- Security:
	- Entries *only* turn up if explicitly set; nothing is set up by default.
		- Example include failed logins and attempts to access protected resources.

Additionally, Domain Controllers and DNS servers have extra logs that are specific to them.

###### Event Types

![[Pasted image 20211210163240.png]]
![[Pasted image 20211210163243.png]]

###### Event Properties

![[Pasted image 20211210163307.png]]

### Real-time monitoring

On Windows, the *Task Manager* provides live real-time information:
- Processor/Memory usage
- Applications/processes
- Network utilisation
- Users connected to a system

However, the task manager can only be used to view information for the local system, and has no logging capability. Even with the use of remote desktop, this makes aggregating information a chore.

#### Performance Console

This is a snap-in that displays real-time data; as well as allowing info to be recorded over time, and actions to be executed when trigger values are reached.

By default, the *Performance Monitor* displays the following:
- Memory
	- Pages/second
- Physical Disk
	- Average disk queue length
- Processor
	- % Processor time

Great care should be taken not to monitor too many metrics, or to observe them too often, as this generates significant overhead. On the other hand, infrequent monitoring risks spikes in values being unrecorded.

![[Pasted image 20211210163729.png]]

##### Performance Logs/Alerts

There are three; *Counter* logs, *Trace* logs and *Alerts:*
- Counter logs capture stats for specified *counters* - to log for later analysis.
- Trace logs record information about system apps when certain events occur.
- Alerts perform actions when a *counter* reaches a specified value.