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
3) Will re-sync the contents between both partitions to create a mirror.



