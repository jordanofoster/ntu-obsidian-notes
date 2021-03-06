# Updating Systems
## Issues with Systems

Naturally, no software is perfect; they are often released too early for commercial reasons, and even mature software can need bug fixes. As a result, networks need coherent and consistent management of changes.

## Servers vs. Workstations

Servers support many users; so update procedures need to be robust. Workstations in comparison only affect individuals - so different strategies may be chosen depending on urgency, type of user, and the number of workstations.

In particular, sysadmins must ask themselves this question; do changes need to be done for *everyone*, or just a few users?

## User Notifications
![[Pasted image 20220112010507.png]]
This method leaves updating mostly to the user; naturally, most will get annoyed, and will never set aside the time to do so themselves (users only use computers when they *need* them to work right then and there.)

## Types of Changes (Microsoft's Terminology)
### Traditional Windows Systems (2k, XP, Vista, 7, 8/8.1)
- Recommended/Optional Updates
	- "*A minor revision to a software product, usually intended to address specific performance issues rather than add new features.*"
- Critical Updates
	- As the name implies, these are urgent.
- Service Packs
	- These are a collection of updates packaged as a single unit, and are *cumulative* - Service Pack 3 contains all changes from Service Packs 1 & 2, using XP as an example.
	- These are not released to any kind of schedule.
- Hotfix
	- These address a very specific issue.

 ### Windows 10/11
 These systems have two release types; feature updates that add new functionality, and quality updates that provide security and reliability fixes.

 #### Servicing Channels

 These are the first way to separate users into deployment groups for feature and quality updates. There are currently *three* release channels for Windows clients.
 - The *General Availability Channel,* which receives feature updates as soon as available.
 - The *Long-Term Servicing Channel,* designed to only be used by specialist devices that don't run office software, and are for the likes of medical equipment or ATM machines. These receive new feature updates every 2-3 years.
 - The *Windows Insider Program* provides organisations with the opportunity to test and provide feedback on features that will be shipped in the next feature update.

### Linux Terminology

Since UNIX is sold and supported, vendors may create custom procedures to distribute software patches (such as Red Hat for enterprise installations). ***This will not be covered by this module.***

*Packages* are a software distribution mechanism that sysadmins can use. Packages can also come in the form of various files and data. 

*Tarballs* are `.tar` files (from **T**ape **Ar**chive) that consist of a sequence of files bundled together for distribution purposes. These are normally compressed. An example of a tarball would be a file called `Update49.tar.gz`, archived into a tarball and compressed with Gzip.

Tarballs can explicitly be pulled off a server and installed by a sysadmin - this is useful when you want direct control, but requires more knowledge and understanding to keep system stability.

Packages allow system updates and changes to be recoverable, as they take account of local configuration changes (and do not overwrite this information), allowing a rollback to previous state if required- higher-level package managers such as `yum` and `apt` make the rollback process even easier.

## An Example of Service Pack Documentation
![[Pasted image 20220112011743.png]]
(Extra notes from lecture?)

### Service Pack Contents
![[Pasted image 20220112011804.png]]

### Windows 10 versions by servicing option
![[Pasted image 20220112011824.png]]

### Windows Support/Knowledge Base

![[Pasted image 20220112011839.png]]

### Windows Server versions by servicing option
![[Pasted image 20220112011902.png]]

## When to update?

For security vulnerabilities, as soon as possible. Hotfixes are only necessary when the issue addressed becomes a problem. Service Packs/Version updates should be installed fairly soon after release, but a small wait is in order to see if the updates have any major issues.

- Service packs offer to backup all files at the start of the installation to `$ntservicepackuninstall$`, allowing rollback if the update causes new problems;
	- The issue is detecting those problems - does the sysadmin have a regression suite to check this, or are they just waiting for user complaints?

On Windows 10 devices, updates are automatically pushed to machines, unless WSUS is setup with Windows 10 Enterprise devices. As a result, things can break and be harder to maintain.

## Checking Security on Windows Systems
![[Pasted image 20220112012343.png]]
The Baseline Security Analyzer (shown above) checks the following for issues:
- OS and its components
- IIS, SQL Server, Office and IE
The program primarily just reports issues, but the version pictured can also update if requested by the sysadmin. It does more checks than basic updater tools, and is container in Server 2008 R2/2012R2 in *Computer Management.*

BSA needs to be installed manually for Windows 7/8.1/10.

## Update Methods

- Users can be allowed to do it via the Microsoft Update site; this is automatic, and the user has no choice under Windows 10 Home. As stated prior, [[Lecture 12 - Updating Systems#User Notifications|this is a bad idea.]]
- Manual installation can be done:
	- For Service Packs, installation is possible via CD or network archive file.
	- Hotfixes can also be chained together.
- Slipstream updating is an older method that involves adding Service Packs/hotfixes as part of the installation process.
- [[Lecture 10 - Managing the Network#Managing the Network|Group Policy]] can be deployed to automate Service Pack inclusion.
- Finally, the Windows Server Update Service (WSUS) can be used.

### Group Policy Objects (GPOs)
[[Lecture 10 - Managing the Network#Group Policy Objects GPO|Group Policy Objects have been covered in Lecture 10.]]

#### GPO Editor
![[Pasted image 20220112013037.png]]
Additional screenshot showing how the [[Lecture 10 - Managing the Network#Group Policy Management Console|GPO Editor]] can be used to automate distribution of update packages.

### Windows Server Update Services (WSUS)
Allowing workstations to automatically update from the Microsoft website can cause a few problems:
- Sysadmins may not wish for all updates to be included
- Internet traffic could be substantial
- Users may get irritated by machines requiring a restart.

The WSUS reduces these problems by allowing sysadmins more control over the update process.

#### WSUS Architecture Overview
![[Pasted image 20220112013338.png]]

##### Server-Side Architecture
![[Pasted image 20220112013353.png]]
##### Client-Side Architecture 
![[Pasted image 20220112013428.png]]

### Updating Linux via Ubuntu
This can be done either with `apt-get update` or the GUI frontend of *Software Updater:*
![[Pasted image 20220112013618.png]]

#### High-Level Package Management Systems for Linux

As with windows, tools are needed for the update process, including:
- The simplification of locating and downloading packages
- Automation of updates/upgrades
- Facilitation of interdependency management

Unlike Windows, however, Linux packages may be in a wide range of locations, and can have interdependencies (although this also happens with hotfixes in Windows).

##### Advanced Package Tool (`apt`)
This is used by Debian and systems based off it (such as Ubuntu, Mint, etc), but is abstracted by the Update Manager on systems that use it.

`apt` is used when a sysadmin needs to install something not in the distro's default repositories; the program searches for repositories by looking at the contents of `etc/apt/sources.list`. This file lists the *what* (binary, source, stable repositories, etc). and *where* (URL, typically).

Using `netselect-apt`, a list of the fastest mirrors within `sources.list` can be found. `apt-get update` refreshes package information, and `apt-get install <package name>` retrieves and installs any new software packages.

