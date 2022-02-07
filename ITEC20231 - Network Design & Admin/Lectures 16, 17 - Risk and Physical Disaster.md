# Risk and Physical Disaster

There are various different scales of disaster that could occur:
- Individual
- Group
- Site
- Regional

## How much to spend?

Most situations can be mitigated or overcome if enough money is spent - but is it worth it, and how do we estimate how much needs to be spent?

The simplest risk model is given by the following equation:

Risk $=$ Cost of incident $\times$  Probability of occurrence

To generate a risk model for all risks to a network, they must be identified.

## Range of Risks - for all businesses

There are a number of risks that must be taken into account:
- Human
- Operational
- Reputational
- Procedural
- Project
- Financial
- Technical
- Natural
- Political

## Estimating Probability

Generally, this is very hard. There are some strategies however. Probability can be estimated from the following information:

- Published information
	- For natural disaster, flood stats, etc., data from the Met Office is used.
	- For technical failures, MTTF figures for components are referenced.
- Historical information (within the company)
	- Fault report forms
	- Purchase orders (how often are replacements bought?)
	- User requests for data restoration

## Mitigating / Managing Risk

Some risks may not be worth eliminating due to the sheer cost required. The strategies for mitigation/management are as follows:

- Use existing assets, changing the way they are organised, used or controlled
- Contingency planning; accept that the event could occur, but ensure the organisation has procedures in place to minimise impact.
- Invest in new resources, including insurance (paying someone else to take the risk) and hardware.

## Risks for individuals/groups

Common risks for users include:
- Accidental deletion of files
- Disk errors
- Theft of a machine
- Death of a desktop/server machine.

All of the above can be reduced in effect by having various forms of redundant storage, which vary in recovery time and the amount of sysadmin intervention required.

### Using technology to help reduce risk

#### Data Redundancy

There are several types of RAID that assist with this:

- Spanned: Multiple disks appear as a single volume.

![[Pasted image 20220207142626.png]]

- Striped (RAID 0): Multiple disks appear as a single volume, but data is written across all drives at the same rate.

![[Pasted image 20220207142705.png]]

#### Disk Redundancy

Other types of RAID target this issue:

- Mirrored (RAID 1): Identical copies are stored on another volume.

![[Pasted image 20220207142828.png]]

- RAID 5: This is a striped disk set with *parity* - this allows the system to continue running in the event of single disk failure.

![[Pasted image 20220207142858.png]]#

RAID can be implemented either via software (built into the O/S) or via hardware (RAID controllers).

##### Problems with Hardware RAID

There are a number of problems with RAID controllers that must be considered:
- Common mode failure.
- Inconsistent failure rates (when compared with the specs).
- Replacement rates are much higher than MTTF figures suggest.
- Write caching is another issue.
- Transactions written by a database to a RAID setup can also be problematic.

##### Software RAID (Windows Server)

Windows Server 2008 allows the use of disk mirroring to provide a RAID-1 software-based configuration. A second, empty disk is needed to have an equal sized volume to the primary disk partition. The process is as follows:

1) Create a new RAID-1 partition using both disks.
2) Highlight the primary OS partition and click "Add Mirror".
3) The OS will re-sync the contents between both partitions to create a mirror.

![[Pasted image 20220207143211.png]]

##### Summary of software-based RAID choices

| Mirrored Volumes (RAID-1) | Striped Volumes with Parity (RAID-5) |
| --- | --- |
| Can protect system or boot partition | Cannot protect system or boot partition |
| Requires two hard disks | Requires a minimum of three hard disks and allows a maximum of 32 hard disks |
| Has a higher cost per MB | Has a lower cost per MB |
| 50% redundancy | 33% maximum redundancy |
| Has good read/write performance | Has excellent read, moderate write performance |
| Uses less system memory | Uses more system memory |

### When things go wrong

RAID is nice, but cannot help in these situations. We need backups to external media - and to protect against disasters (floods, fires, etc.), we need off-site storage of the backup media.

Offsite provision of spare processing can help when computers are lost, stolen or damaged, but it is costly. Total backup solutions are provided by external data warehouses, but they factor their own risk into their services (and thus cost a lot of money).

####  Backup

Backing up data follows a simple recipe:
1) Use a backup device (DVD, Tape, Drive...)
2) Use a backup software tool (3rd-party tools may be more sophisticated)
3) Knowledge of *what* exactly to backup

Hardware considerations for 1) include:
- Capacity
- Speed
- Cost
- Reliability

##### Types of Backup

- Normal/Full
	- This backs up a complete copy of the target folder/drive.
- Incremental
	- This clears the *archive* bit on all files.
	- Only files marked as *changed* will be included in the next backup.
- Differential
	- This does not clear the archive bit on files...
	- ...and backs up all files since the last *full* backup.

Note that if multiple copies of the same data is stored, space used can be reduced via deduplication (i.e. having multiple references to a single copy of the data).

###### Incremental Backup Example

Suppose that an incremental backup is performed on Tuesday; only the data that changed since Monday's incremental backup will be backed up today. The result is a much smaller and faster backup; with the advantage of a shorter time interval between backups, and less data itself to be backed up.

![[Pasted image 20220207144037.png]]

###### Differential Backup Example

Suppose that a full backup is done on Sunday. On Monday, only files that have changed since Sunday are backed up; on Tuesday, only the files that changed since Monday are backed up, and so on until the next full backup is performed.

![[Pasted image 20220207144156.png]]


###### Example of Alternative Backups

| Day | Backup | Contents | Comment |
| --- | --- | --- | --- |
| 1 | | Full | A,B,C | A,B then changed |
| 2 | Incremental | A,B only | C changed, D created |
| 3 | Incremental | C,D only | Keeps backup small |
| 1 | Full | A,B,C | A,B then changed |
| 2 | Differential | A,B only | C changed, D created |
| 3 | Differential | A,B,C,D | Backs up all changes since Full |

###### Example of Alternative Full Restorations

A failure occurs on Day 3 of backups:

- Using the incremental strategy:
	- Restore Day 1's Full Backup
	- Restore Day 2's Incremental Backup
	- Restore Day 3's Incremental Backup
- Using the differential strategy:
	- Restore Day 1's Full Backup
	- Restore Day 3's Differential Backup

##### Incremental vs Differential

Incremental backups take up much less storage space and can be run much faster; but recovery is slower as you have to deal with many more 'pieces' in the form of the increments. Differential backups take up a fair amount of storage space by comparison; while they are faster than full/normal backups, they are slow compared to incremental backups.

##### Other backup Strategies

There are various strategies for rotating out backup media. Grandfather-Father-Son (GFS) rotation is a widely used strategy for storage media. It works as thus:

- Daily (Son): 
	- Reuse every week, store backups on 7 separate pieces of media (1 week's worth).
- Weekly (Father): 
	- Reuse every month, store backups on 4 separate pieces of media (1 month's worth).
- Monthly (Grandfather): 
	- Reuse every year, store backups on 12 separate pieces of media (1 year's worth).

Other backup strategies include the *Tower of Hanoi* method.

##### Backup & Restore under Linux

Linux can use the `dump` and `restore` commands, but dumps cannot be applied directly to a remote disk. Nemeth (et al) recommend `Bacula` as a network/site wide solution for enterprises, due to the following reasons:
- It backs up data from a wide range of O/Ses.
- It uses MySQL or other systems as a backend database.
- It can write backups that span multiple tape volumes.
- It handles auto changers.
- It can write MD5 checksums to validate files.
- It's free!
- Bacula is very complex, but rich in features such as scheduling.

###### Bacula Structure
![[Pasted image 20220207145245.png]]

##### Backup Security

Nemeth quotes Dan Geer in saying the following:
*"What does a backup do? It reliably violates file permissions at a distance."*

Thus, the following should be done to keep backups secured:
- Create specific user accounts for backup purposes
	- For example, members of the *Backup Operators* group can backup files without having NTFS read permissions.
- Password-protect tapes - though this might be a problem if different software is used to recover the backup.
- Store and transport backups securely.
- Possibly encrypt the data being backed up.

## System Disasters

If the entire Windows OS dies, an ASR backup should be ready for use. ASR backups cover system files, system data, system services, etc. It should be noted that an ASR backup does *not* backup user data.

ASR backups reformat the entire system drive when restored, and as such should only be used if all else has failed.

Plenty of linux systems are available via a bootable CD or USB drive, so recoveries can be done from here.

Alternatively, the cloud may be used

