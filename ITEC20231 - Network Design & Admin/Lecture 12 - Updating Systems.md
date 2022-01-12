# Updating Systems
## Issues with Systems

Naturally, no software is perfect; they are often released too early for commercial reasons, and even mature software can need bug fixes. As a result, networks need coherent and consistent management of changes.

## Servers vs. Workstations

Servers support many users; so update procedures need to be robust. Workstations in comparison only affect individuals - so different strategies may be chosen depending on urgency, type of user, and the number of workstations.

In particular, sysadmins must ask themselves this question; do changes need to be done for *everyone*, or just a few users?

### User Notifications
![[Pasted image 20220112010507.png]]
This method leaves updating mostly to the user; naturally, most will get annoyed, and will never set aside the time to do so themselves (users only use computers when they *need* them to work right then and there.)

### Types of Changes (Microsoft's Terminology)
#### Traditional Windows Systems (2k, XP, Vista, 7, 8/8.1)
- Recommended/Optional Updates
	- "*A minor revision to a software product, usually intended to address specific performance issues rather than add new features.*"
- Critical Updates
	- As the name implies, these are urgent.
- Service Packs
	- These are a collection of updates packaged as a single unit, and are *cumulative* - Service Pack 3 contains all changes from Service Packs 1 & 2, using XP as an example.
	- These are not released to any kind of schedule.
- Hotfix
	- These address a very specific issue.

 #### Windows 10/11
 These systems have two release types; feature updates that add new functionality, and quality updates that provide security and reliability fixes.

 ##### Servicing Channels

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

###