# Managing the Network

## Group Policy Objects (GPO)

![[Pasted image 20211129211236.png]]

A GPO applies rights or limitations to all the AD objects in a container (or set of containers). A container may be a site, domain or organisational unit (OU) - GPOs are *not* directly applicable to groups!

The aim of GPOs is to simplify management of networks with reference to rules that apply to multiple users and/or machines.

### GPO Applicability

GPO's can control settings for software configuration, registry, security configuration, software installation and lots more. GPOs have a hierarchy; higher levels overrule lower levels.

Filtering/delegation can be applied to limit scope/customise, but there are some cases where GPOs fail to apply - and this can be tricky to debug.

#### Who is allowed to set them?

The relevant predefined Active Directory GLOBAL groups are:
- Domain Admins
- Enterprise Admins (only appear in Forest root domain)
- Group Policy Creator Owners (by default, domain admin acct is member of this group)
- However, by default, predefined AD groups only get rights/permissions when added to domain local groups.

Every AD domain has a built-in container where it creates security groups with domain local scope. These have the relevant rights are permissions.

The most important group here is Administrators - by default, the global Enterprise and Domain Admin groups are added to this. Administrators have large sets of RIGHTS by defaults, though these may be delegated to others.

### Group Policy Management

There can be lots of GPOs within a domain; the Group Policy Management Console provides you with a way to manage these GPOs by providing access to the Group Policy Editor, where individual policy objects can be created and edited, alongside access to Administrative templates (.admx) which describe where registry-based group policy settings are stored, and are used to change settings on GPOs.

#### Group Policy Management Console

![[Pasted image 20211129212106.png]]

#### Administrative Templates

There are a number of templates that are built-in, stored within .admx files, that use XML to describe settings. Each of these files contain many individual policy descriptions, and where they are stored in the Registry.

If an admin wants to add new policies, Microsoft recommends creating custom .admx files rather than modify the existing templates.

![[Pasted image 20211129212254.png]]

This is done by entering `%systemroot%` in a runbox and going to the PolicyDefinitions directory - where there are lots of admx files.

##### Example Policies in .admx

- Enable disk quotas
- Enforce disk quota limit
- Default quota limit and warning level
- Log event when quota limit exceeded

- Scripting of Java applets
- Logon options
- Run .NET Framework-reliant components signed with Authenticode
- Run .NET Framework-reliant components not signed with Authenticode
- Download signed ActiveX controls
- Download unsigned ActiveX controls

- Configure Automatic Updates
- Specify Intranet Microsoft update service location
- Enable client-side targeting
- Reschedule Automatic Updates scheduled 
- No auto-restart for scheduled Automatic Updates
- installations

#### Security Policies (secpol.msc)

![[Pasted image 20211129212958.png]]

### Effect of not using GPO for accounts
   
In January 2009 (and more since!), a hacker gained access to a Twitter employee???s administrative account and was able to use the admin tools to reset passwords on other users??? accounts. Then these passwords for the accounts of several celebrities (including Barack Obama) were published on a hackers??? forum. Subsequently, posts were made on those accounts by unauthorized persons. Twitter did not use account lockout policies to prevent a hacker from utilising dictionary attacks.

Miley Cyrus had her Twitter account suspended temporarily after it was hacked into, and offensive messages posted.

In the case of the hacked Twitter employee, the combination of a weak password, "happiness???, and Twitter's lax security regarding repeated login attempts made it simple for the hacker to gain entry. Twitter has not indicated that it has fixed this vulnerability by limiting the number of password attempts.

One individual observed the following about the Miley Cyrus incident:

*"It appears that Miley didn't learn the lesson last year and hasn't been taking enough care over her password security to avoid the same fate, other users should make sure they choose strong passwords that can't be easily cracked, and Twitter itself should play a key part in enforcing this."*

*?????? I started wondering how vulnerable other sites might be to this type of attack.?? ??? I went looking at some of the sites that I frequent and found that many of them don???t have any restrictions on authentication attempts???*

*And how hard would it really be to create such a script to attempt a brute force attack like the one that was used by the hacker??? Well??? How about four simple lines of code attached to a very large dictionary database:???*

```
Set WinHttpReg = CreateObject("WinHttp.WinHttpRequest.5.1")
WinHttpReq.Open "POST","http://domain.com/login",false
WinHttpReq.SetRequestHeader "Content-Type","application/x-www-form-urlencoded"
WinHttpReq.Send("login=Chris&password=Pa$$w0rd")
```

*???I tested this script against a site that I frequent, and it worked as expected.?? So, I guess it???s not that hard to perform such an attack.?? Now it seems the question isn???t how did this happen to Twitter, but why doesn???t this happen every day????*

#### Example security issue helped by GPO

A particular problem is the need to disable USB sticks and other removable media in secure installations. You can set up custom .admx files to include this, and apply them via GPO to a group of workstations. This disables various drivers, and generally works a lot better than gluing up the USB ports.

Windows includes extensions to GPs to make this easier such as *Removable Storage Management,* but also includes approximately 800 other new policy settings.

#### Other Issues with GPO's 

For earlier versions of Windows Server and Windows, they run in *winlogon* and then update on irregular time basis. This is still relevant to know as there are still a number of Windows 2003 Servers and XP machines in corporate networks/embedded systems.

However, for Windows 10 and newer versions of Windows Server, they have their own ???hardened??? (dedicated) service which cannot be stopped.

.admx files are added to sysvol every time a new GPO is created ??? this can lead to lots of copied files around the system, and replication traffic overhead.

Some of the GPO???s have to be considered as merely obscuration rather than security, since users may be able to use other programs to get around them e.g. for editing Registry settings

#### Managing Software on the Network

GPOs allow admins to specify which .msi packages are to be assigned or published. Assignment can be user or computer associated, whereas publishing is necessarily linked only to users (a user has to do something to install it). GPOs can also define how upgrade/removal of software is handled.

![[Pasted image 20211129215829.png]]

##### Why .msi?

- Contains useful info about structure of program
- Can self-heal if files accidentally deleted
- Installer creates system restore point before installing - so reverts automatically if install goes wrong
- Has sophisticated options for various methods of installation -especially for big programs and slow links - to install only some bits of large packages (e.g. Office) immediately.

#### How to setup and use

- Create Software Distribution Points (SDP) - shared network folders with NTFS Read/Execute permissions for the users
- Create GPO for software deployment (and associate with chosen domain/site/OU)
- Configure software deployment properties for the GPO - location of SDP, default handling of new packages, etc.
- Add the installation packages to the GPO (indicating whether to be published or assigned)
- Configure each installation package properties - e.g.
	- Auto-Install This Application By File Extension Activation
	- Uninstall This Application When It Falls Out Of The Scope Of Management

##### Some snags

- No licence control is performed - so published software had better be on a site licence.
- Need to plan carefully how to structure the software e.g. common packages to be assigned to computers, specific ones to be assigned to different user groups etc., otherwise might have too many GPOs to manage
- If users need admin privilege to install, risky! Can configure installer to "always install elevated", but this also poses a security risk.

#### Microsoft Software Licensing

- Needs care in Windows networks
- Need to consider whether Per User or Per Device is the most cost-effective way.
	- Also, might need to buy additional Client Access Licences for Remote Desktop Services if remote users log in to a server
- Each 2008+ Server computer runs a Licence Logging service, which keeps track.
- The information is replicated to a Site Licence Server
- Can maintain licence information for file, print services, IIS, RDS, Exchange, SQL Server etc.

#### Process to maintain licences

- Identify Site Licence Server (normally first domain controller in a site)
- Administer licences using Licensing in Administrative Tools
- To add new licences, select New Licence, and specify added 
- Alternatively, use 3rd party tool that can also handle other licences e.g. volume
- Monitor licence status regularly


