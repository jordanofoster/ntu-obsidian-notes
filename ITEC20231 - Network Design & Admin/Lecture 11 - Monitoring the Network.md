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

Alternatively remote administration can be done via PowerShell, with the use of `ssh` required on 