# Permissions

## Group Types

When defining a group, its type must be considered - this dictates what it can and cannot do (i.e. security and permissions of the group). There are four basic types:

- **Distribution groups**
	- Used when limited access to a resource is required (e.g. in MS Exchange Server for sending emails to groups).
- **Security groups**
	- Admins mostly use security groups to specify permissions a group has when interacting with a resource.
- **Application basic groups**
	- These groups consist of LDAP query groups, Windows users/groups, and other basic application groups.
- **LDAP query groups**
	- Membership in these groups is dynamically calculated as needed from Lightweight Directory Access Protocol (LDAP) queries. LDAP query groups are types of application group.

LDAP is an application protocol for querying and modifying items in directory service providers such as Active Directory (which supports a form of LDAP). AD is a directory service database, and LDAP is one of the protocols used to talk to it.

### Group Scope

Groups have a *Scope*. Depending on its scope, a group can be assigned permissions to different extents within the domain structure. There are three types of scope, as outlined in the table below:

| Group Scope | Group Membership Can Include (Microsoft 2021) | Can be used to (Microsoft, 2021) |
| ----------- | --------------------------------------------- | -------------------------------- |
| Domain Local | User accounts from any domain in the forest; global groups or universal groups from any domain in the forest; user accounts or global or universal groups from any domain in trusted forest; nested domain local groups from the local domain. | Assign access to resources only in the local domain; on all servers in domain running Windows Server 2000 to 2022. |
| Global | User accounts from the domain where the group is created; nested global groups from the local domain. | Assign access to resources in all domains in forest or between trusted forests; member servers running Windows Server. |
| Universal | User accounts from any domain in forest; global groups from any domain in forest; nested universal groups from any domain in forest. | Assign access to resources in all domains in forest or between trusted forests; on all servers running 2000 + |

#### Domain Local Groups

These are available even in lower domain functional levels and are typically assigned permissions to resources, such as shared folders or printers, then allowing easier group nesting.

DLGs can also be used to group users from the same domain needing the same permissions to access a resource in the same domain. They can *only* be used to assign permissions to resources in the domain in which they were created.

#### Global Groups

Global groups are often used to gather both users and computers together in the same domain with the same role or function, or requiring similar access requirements.

GGs can only include members from within their own domain, including other GGs from the same domain. They can be granted permissions for resources in any domain in the forest, and in *trusted* domains in other forests.

GGs are not replicated outside of their own domain; using them minimises replication traffic to the global catalogue. They are used for objects that require frequent maintenance, such as user/computer accounts.
 
 #### Universal Groups
 
 These are used mainly to grant access to related resources over multiple domains (e.g. if executives need access to printers throughout the network). UGs are mainly used to consolidate groups that span multiple domains, and are unneccessary in single-domain networks.
 
 The best practice for implementing UGs is as follows:
 - Create a GG in each domain for user or computer accounts, then the UG contains the GGs.
	 - Avoids too much replication traffic since UG membership changes infrequently.

##### Global & Domain Local Groups - Planning (Summary)

1. Create DLGs for shared resources (e.g. a group for a set of colour printers)
2. Assign resource permissions to domain local group (e.g. Whatever permissions needed to use printers)
3. Create GGs for users with common roles (e.g. Accounts or Sales)
4. Add GGs into appropriate DLGs (e.g. to give Sales access to the specialist printers)

#### Group Scope and Functional Levels

 Group scope is affected by the *Functional Level* of the domain in which it exists, which is dictated by the lowest version of windows server running as a DC within the domain; this can also dictate the functional level of a forest.

##### Domain Functional Levels (DFLs)

The table below summarises the long changelog in the following sections:

| Functional Level | Features (Microsoft, 2021) |
| ---------------- | -------------------------- |
| Windows 2000 Native | Universal groups enabled for distribution and security groups; group nesting; group conversion; SID history. |
| Windows Server 2003 | Domain rename; last logon timestamp; password setting on inetOrgPerson / User objects; redirect users/computers containers; authorisation manager policies; constrained delegation; selective authorisation. |
| Windows Server 2008 | Distributed File System replication of SYSVOL; Advanced Encryption Services for Kerberos; interactive logon info; fine-grained password policies |
| Windows Server 2008 R2 | Authentication mechanism assurance; Automatic SPN management |
| Windows Server 2012 | KDC support for cliams, compound authentication |
| Windows Server 2012 R2 | DC-side protections for Protected Users; Authentication Policies; Authentication Policy Silos |
| Windows Server 2016 | DCs can support rolling a public key only user's NTLM secrets; DCs can support allowing network NTLM when a user is restricted to specific domain-joined devices; Kerberos clients successfully authenticating with the PKInit Freshness Extension will get the fresh public key identity SID. |
| Windows Server 2019 | There are no new domain functional levels added in this release. |

###### Windows 2000 Native

All of the default ADDS features are available alongside the following directory features:
- Universal groups for both distribution and security groups
- Group nesting
- Group conversion, allowing conversion between security/distribution groups
- Security identifier (SID) history

###### Windows Server 2003

All of 2000's features are available (as well as default ADDS), but 2003 includes:

- `Netdom.exe`, a domain management tool that allows DCs to be renamed
- Logon timestamp updates
	- The `lastLogonTimestamp` attribute is updated with the last logon time of the user/computer, and is replicated within the domain.
- `userPassword` attribute can be set as the effective password on `inetOrgPerson` and user objects
- User/Computers containers can be redirected
	- By default, two well-known containers are provided, named `cn=Computers,<domain root>` and `cn=Users,<domain root>`. This features allows a new well-known location to be defined for these accounts.
- Authorization Manager can store its authorization policies in ADDS
- Constrained delegation
	- Makes it possible for application to take advantage of secure delegation of user credentials using Kerberos-based authentication.
	- Delegations can be restricted to specific destination services only.
- Selective authentication
	- Allows specification of users/groups from trusted forests who are allowed to authenticate to resource servers in a trusting forest.

###### Windows Server 2008

Includes default ADDS, 2003's features, and the following:

- Distributed File System (DFS) replication support for Windows Server 2003 System Volume (SYSVOL)
	- DFS replication provides more robust and detailed replication of SYSVOL contents.
		- Beginning with 2012 R2, File Replication Service (FRS) is deprecated. New domains created on a DC that runs >= 2012 R2 must be set to the 2008 DFL or higher.
- Domain-based DFS namespaces running in 2008 mode, which includes support for access-based enumeration and increased scalability. Domain-based namespaces in 2008 mode also require the forest to use the 2003 forest functional level. More information in [Choose a Namespace Type](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770287(v=ws.11))
- AES128/256 support for Kerberos protocol. In order for TGTs to be issued with AES, DFL must be 2008 or higher and domain password needs to be changed.
	- More information in [Kerberos Enhancements](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-vista/cc749438(v=ws.10))
	- Authentication errors may occur on a DC after the domain functional level is raised to 2008 or higher if the DC has already replicated the DFL change but not yet refresehed the `krbgt` password. In this case, restarting the KDC service on the DC will trigger an in-memory refresh of the new `krbgt` password and resolve related authentication errors.
- [Last Interactive Logon](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd446680(v=ws.10)) Information displays following information:
	- Total number of failed logons at domain-joined 2008 server or Vista workstation
	- Total number of failed logons after successful logon to 2008 server or Vista workstation
	- Time of last failed logon attempt at a 2008 server or Vista workstation
	- Time of last successful logon attempt at 2008 server or Vista workstation
- Fine-grained password policies make it possible to specify password/account lockout policies for users/global security groups in a domain. For more information check [Step-by-Step Guide for Fine-Grained Password and Account Lockout Policy Configuration](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770842(v=ws.10)).
- Personal Virtual Desktops
	- To use added functionality provided by the PVD tab in the User Account Properties dialog bog in AD Users and Computer, your ADDS schema must be extended for 2008 R2 (schema object version = 47). For more information see [Deploying Personal Virtual Desktops by Using RemoteApp and Desktop Connection Step-by-Step Guide](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941616(v=ws.10)).

###### Windows Server 2008 R2

Default ADDS and 2008's functional level features, plus:
- Authentication mechanism assurance, packaging information about type of logon method (smartcard/username+password) used to authenticate domain users inside each user's Kerberos token. When enabled in a network environment that has deployed a federated identity management infrastructure such as AD Federation Services, the info in the token can then be extracted whenever users attempt to access claims-aware applications that have been developed to determine authorization based on user's logon method.
- Automatic SPN management for services running on particular computers under the context of a Managed Service Account when the name or DNS host name of the machine account changes. Check [Service Accounts Step-by-Step Guide](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356(v=ws.10)) for more information.

###### Windows Server 2012

All ADDS features and 2008R2's functional level features, including:
- KDC support for claims, compound authentication and Kerberos armoring KDC admin template policy has two settings (*Alawys provide claims* and *Fail unarmored authentication request*) that require 2012 DFL. For more information, [What's New in Kerberos Authentication](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11))

###### Windows Server 2012 R2 

All ADDS, 2012 features, including:

- DC side protections for Protected Users. Protected Users authentication to a 2012R2 domain can no longer:
	- Authenticate using NTLM
	- Use DES or RC4 cipher suites with Kerberos pre-authentication
	- Be delegated with unconstrained/constrained delegation
	- Renew user tickets (TGTs) beyond initial 4 hour lifetime
- Authentication Policies
	- New forest-based AD policies which can be applied to accounts in 2012R2 domains to control which hosts an account can sign-on from and apply access control conditions for authentication to services running as an account.
- Authentication Policy Silos
	- New forest-based AD object which can create relationship between user, managed service and computer; accounts to be used to classify accounts for authentication policies or authentication isolation.  

###### Windows Server 2016

All ADDS, 2012R2 features, including:
- DCs can support automatic rolling of NLTM and other password-based secrets on user accounts configured to require PKI authentication. Also known as *Smart card required for interactive logon*
- DCs can support allowing network NLTM when user is restricted to specific domain-joined devices.
- Kerberos clients successfully authenticating with PKInit Freshness Extension will get fresh public key identity SID.
- For more info: [What's New in Kerberos Authentication](https://docs.microsoft.com/en-us/windows-server/security/kerberos/whats-new-in-kerberos-authentication) and [What's new in Credential Protection](https://docs.microsoft.com/en-us/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

###### Windows Server 2019

No new forest or domain functional levels added in this release. Minimum requirement to add 2019 DC is a 2008 DFL. Domain also has to use DFS-R as engine to replicate SYSVOL.

##### Forest Functional Levels (FFLs)

| Forest Functional Level | Features (Microsoft, 2021) |
| ----------------------- | -------------------------- |
| Windows 2000 | Default AD feature set |
| Windows Server 2003 | Forest trust; domain rename; linked value replication; Read-only domain controllers (RODC); improved knowledge consistency checker; dynamic objects; deactivation/redefinition of attributes and classes in schema. |
| Windows Server 2008 | No additional forest level features; will default to a Server 2008 FL instead of a 2003 FL. |
| Windows Server 2008 R2 / 2012 / 2012 R2 | Active Directory Recycle Bin |
| Windows Server 2016 | Privileged access management (PAM) using Microsoft Identity Manager (MIM) |
| Windows Server 2019 | There are no new forest functional levels added in this release.

###### Windows 2000 Native

All default ADDS features are available.

###### Windows Server 2003

All default ADDS features alongside the following:

- Forest trust
- Domain renaming
- Linked-value replication
	-    Linked-value replication makes it possible for you to change group membership to store and replicate values for individual members instead of replicating the entire membership as a single unit. Storing and replicating the values of individual members uses less network bandwidth and fewer processor cycles during replication, and prevents you from losing updates when you add or remove multiple members concurrently at different domain controllers.
	- The ability to deploy a read-only domain controller (RODC)
- Improved Knowledge Consistency Checker (KCC) algorithms and scalability
	- The intersite topology generator (ISTG) uses improved algorithms that scale to support forests with a greater number of sites than AD DS can support at the Windows 2000 forest functional level. The improved ISTG election algorithm is a less-intrusive mechanism for choosing the ISTG at the Windows 2000 forest functional level.
- The ability to create instances of the dynamic auxiliary class named `dynamicObject` in a domain directory partition
- The ability to convert an `inetOrgPerson` object instance into a User object instance, and to complete the conversion in the opposite direction
- The ability to create instances of new group types to support role-based authorization.
	- These types are called application basic groups and LDAP query groups.
- Deactivation and redefinition of attributes and classes in the schema. The following attributes can be reused: `ldapDisplayName`, `schemaIdGuid`, `OID`, and `mapiID`.
- Domain-based DFS namespaces running in Windows Server 2008 Mode, which includes support for access-based enumeration and increased scalability. For more information, see [Choose a Namespace Type](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770287(v=ws.11)).

###### Windows Server 2008

All features available in 2003 are present, but no additional features added.

###### Windows Server 2008 R2

All features available in 2003, plus the following:

- Active Directory Recycle Bin, which provides the ability to restore deleted objects in their entirety while AD DS is running

###### Windows Server 2012

All features available in 2008 R2 present, but no additional features added.

###### Windows Server 2012 R2

All features available in 2012 present, but no additional features added.

###### Windows Server 2016

All features available in 2012 R2, plus the following:

- [Privileged access management (PAM) using Microsoft Identity Manager (MIM)](https://docs.microsoft.com/en-us/windows-server/identity/whats-new-active-directory-domain-services)

###### Windows Server 2019

No new FFLs or DFLs added in this release.

### Permissions

Permissions are a privilege granted to a user/group/computer to perform a particular action or access a particular resource. Windows Server has many different sorts of permissions, though the most visible are:

- **File-system** access to files & folders under NTFS.
- **Share** access to file system and printer shares.
- **AD** access to Active Directory objects.
- **Registry** access to registry keys.

All of these are separate and different.

#### Access Control Lists (ACLs)

An Access Control List is associated to an object being accessed, and not the object accessing it. It lists all permissions that can access that object (e.g. users/groups/etc.) and also lists what operations can be done to the object.

Lists are made out of Access Control Entries (ACEs), i.e. the name of the security principle and the permissions it has been granted. An example is shown below:

![[Pasted image 20211115214501.png]]

#### NTFS Permissions

Standard permissions can mostly be used for NTFS files and folders (e.g. Read/Read & Execute/Write/Modify/List Folder Contents/Full Control) - although occasionally more fine-grained permissions must be setup using the 14 NTFS Special Permissions; the Standard permissions are just a convenient grouping into the most frequently used sets.

Slight differences apply when permissions are applied to a file rather than a folder; for example, it is obvious that List Folder Contents is not a permission applicable to files.

##### NTFS Special Permissions

1. Traverse Folder/Execute File
2. List Folder/Read Data
3. Read Attributes
4. Read Extended Attributes
5. Create Files/Write Data
6. Create Folders/Append Data
7. Write Attributes
8. Write Extended Attributes
9. Delete Subfolders and Files
10. Delete
11. Read Permissions
12. Change Permissions
13. Take Ownership
14. Full Control

###### Example Permissions
![[Pasted image 20211115214856.png]]

###### Access to Special Permissions

![[Pasted image 20211115214918.png]]

##### Example Permissions Breakdown

*Read & Execute* is comprised of the following of the 14 NTFS Special Permissions:

- List Folder/Read Data
- Read Attributes
- Read Extended Attributes
- Read Permissions
- Synchronise
- **Traverse Folder/Execute File**
	- *Traverse Folder* lets security principles move through inaccessible folders to reach folders/files they are allowed to access. Without this permission, only *Read* Standard Permissions are granted.

#### Inheritance Rules for Permissions

By default, subordinate objects inherit permissions that their parent possesses. For example, if a user is granted permission to the root of a drive, then they have the same permission on all files and subfolders.

Inheritence can be counteracted by either turning it off when working with special permissions or denying permissions explicitly.

#### Precedence Rules for Permissions

Allowed permissions are cumulative; all of the permissions of a security principal combine to give the **Effective Permissions.**

Denied permissions override allowed permissions; Explicitly denying permissions overrides allowed permissions from **any other source.**

Explicit permissions take precedence over inherited permissions, so **explicitly** allowed permissions override **inherited** denied permissions.

##### Permissions Can Get Complicated

As a result, a user's permissions are a combination of those inherited from their group membership and any given to them explicitly, but this is not directly shown in the *Properties* window since it shows separate groups, etc. As an example:

- User `cmp3lambes` is granted the **Allow Read & Execute** permission on a folder called **ModuleSpecs.** But `cmp3lambes` is also a member of the **Lecturers** groups, which has been granted **Allow Full Control** and the **Everyone** group, which grants **Allow Read.**
- As a result, `cmp3lambes` has an effective permission of **Allow Full Control** on this specific folder.

###### Effective Permissions

The effective permissions view is used to make visualization of scenarios such as the above easier.

![[Pasted image 20211115215953.png]]

### Registry Keys

Registry Keys are the entities that store information about a Windows PC. They are used for:

- Hardware information
- OS information
- Non-OS programs
- Users
- Preferences

#### Registry Structure and Use

The Registry is separated into *Hives:*

###### `HKEY_CLASSES_ROOT`
![[Pasted image 20211115220234.png]]
This is used for installed apps - file associations, etc.

######  `HKEY_CURRENT_USER`
This includes specific settings for the current user, such as printer settings.

###### `HKEY_LOCAL_MACHINE`
This is general to all users and include information such as driver versions.

###### `HKEY_USERS`
This includes details of all user profiles keys that can access the machine. `Current_User` is a partial list of this information.

###### `HKEY_CURRENT_CONFIG`
This is generated at boot time to give information about the local machine configuration.

#### Registry Entries

![[Pasted image 20211115220514.png]]

For registry entries to be modified, the program or user has to be allowed to change it. In the image above, we see the Administrators group has been given Full Control over this sub-key, via inheritance.

#### Registry Permissions
![[Pasted image 20211115220655.png]]
(Note: Write DAC = ability to change ACL for key)

There are both similarities and differences between these and NTFS permissions; for starters, a different set of standard and special permissions. Inheritance can be again allowed or stopped, and deny/allow priority applies.

Discretionary Access Control (DAC) allows a user or administrator to define an ACL on a specific resource (e.g. file, registry key, database table, OS object, etc).

#### Why of interest in a network?

Various programs may need to run on a server which must have appropriate access to registry keys. If users want applications installed locally, problems can also occur if the registry keys do not have appropriate ACLs set.

### Active Directory Object Permissions

These are again very different to NTFS and Registry permissions, e.g.:

- **Create child**
- **Delete child**
- **Standard delete**
- **Delete tree**
- **Read property**
- **Write property**

Microsoft's general advice is to recommend not changing these, as if they are, performance can be lost due to the amount of information transmitted around the network.

#### Who can create file system shares?

This depends on the role of the machine and therefore the security risks associated with doing so:

- Domain Controllers:
	- Only the following groups:
		- Administrators
		- Server Operators
		- Enterprise Admins
		- Domain Admins
- Domain Member Server or Workstation:
	- Only the following groups:
		- Administrators
		- Server Operators
		- Power Users
	- Workgroup or Standalone computer:
		- Only the following groups:
			- Administrators
			- Power Users

##### Microsoft File Shares

These allow network clients to actually see folders on a network remotely; some shares are created automatically due to the role of a server; for example `NETLOGON` shares are created when a system becomes a domain controller.

![[Pasted image 20211115221511.png]]
`NETLOGON`: Windows Server service that authenticates users and other services within a domain
`SYSVOL`: Set of files and folders that reside on local hard disk of each DC in a domain that are replicated by the File Replication Service (FRS).

Shares can be hidden by appending $ to the name, but this poses an issue: how do users find it? By creating a share using the MMC Shared Folders Snap-in, shown below:

![[Pasted image 20211115221804.png]]

###### File Share Permissions

These differ from NTFS, with a much coarser grain, having no special permissions.

Changes in the Share Permissions are *not* the same as *modify* in NTFS in the delete area. When both Share and NTFS permissions are present, the resultant that is applied is the *most restrictive.*

File share permissions should *not* apply to locally logged on users (e.g. physically local or by Terminal Server).

###### Limitations/Issues

- **Limited scope** - Can be applied only to folders, and only when connecting to the share.
- **Lack of flexibility** - Permissions applied to the share apply to all levels below.
- **No replication** - Share permissions are not replicated by the DC.
- **No resiliency** - Shares (and by extension, Share permissions) are lost when a folder is moved or renamed.
- **No auditing possible**
- **Do not show up in Effective Permissions tab** - As a result they need to be looked at independently and then considered with NTFS permissions to give the resultant most restrictive.

#### Old UNIX/Linux Permissions

Each file has a set of bits that specify its permissions for 3 classes of user; **Owner, Group Owner** and **Everyone Else.** The owner is special, being able to totally limit access. 

Each class has 3 bits; `r` (read), `w` (write), `x` (execute). These are expressed as `rwx` if allowed, or a `-` if not allowed (e.g. `rwxr-xr-x` means owner allowed all 3, but all others only allowed to read and execute.)

The superuser `root` can do anything even if not the owner of the file.

##### Examples of Linux Permissions

![[Pasted image 20211115223119.png]]

#### Modern UNIX/Linux Permissions

Modern distributions now support ACLs, partly for compatibility with Windows via SAMBA. File permissions themselves are still based on read/write/execute, however (not as fiddly as NTFS, so SAMBA has to 'translate' between them).

ACLs allow rwx to be set for multiple groups and specific users.

(`SAMBA`:    Open source powerful server that helps you to share files and printers with Windows-based and other operating systems. Can also integrate with a Microsoft Windows Server domain, either as a Domain Controller (DC) or as a domain member.)

### Printer Server Topologies

For cost effectiveness, we want multiple users to access a single printer. What options do we have?

1. **Locally Attached Printers**
2. **Network Attached Printers**
	1. **Logical printer on every client workstation**
		1. **Logical Printer** - object used by operating system to represent physical device. Contains settings, defaults, drivers and other properties.
	2. **Print Server **
			1. **Print server** - recieves jobs from clients, stores them in print queue and sends 1-by-1 to physical printer

#### Locally Attached Printer  (LAP)

![[Pasted image 20211115222546.png]]

This presents physical security issues, as the printer has to be close to the server. When the printer share is created, the attached server functions as the print server.

#### Network attached printer, with logical printer on every client

![[Pasted image 20211115222636.png]]

##### Issues

- Each user only sees their own jobs, not the rest of the cue - this might cause lots of waiting.
- Admins cannot manage the print queue or implement advanced features.
- Error messages only appear on the user machine.
- If a driver update is required, it has to be done on each client.
- Print processing is not offloaded to the server.

#### Network attached printer, with print server

![[Pasted image 20211115222811.png]]