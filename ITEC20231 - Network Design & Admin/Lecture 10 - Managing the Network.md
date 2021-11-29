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

If an admin wants to add new policies, Microsoft recommend to creaete custom .admx files rather than modify the existing templates.

![[Pasted image 20211129212254.png]]

This is done by entering `%systemroot%` in a runbox and going to the PolicyDefinitions directory - where there are lots of admx files.

##### Example Policies in .admx

- Enable disk quotas
- Enforce disk quota limit
- Default quota limit and warning level
- Log event when quota limit exceeeded

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
- No auto-restart for schedulded Automatic Updates
- installations

#### Security Policies (secpol.msc)

![[Pasted image 20211129212958.png]]

### Effect of not using GPO for accounts
   
In January 2009 (and more since!), a hacker gained access to a Twitter employee’s administrative account and was able to use the admin tools to reset passwords on other users’ accounts. Then these passwords for the accounts of several celebrities (including Barack Obama) were published on a hackers’ forum. Subsequently, posts were made on those accounts by unauthorized persons. Twitter did not use account lockout policies to prevent a hacker from utilising dictionary attacks.

Miley Cyrus had her Twitter account suspended temporarily after it was hacked into, and offensive messages posted.

In the case of the hacked Twitter employee, the combination of a weak password, "happiness“, and Twitter's lax security regarding repeated login attempts made it simple for the hacker to gain entry. Twitter has not indicated that it has fixed this vulnerability by limiting the number of password attempts.

One individual observed the following about the Miley Cyrus incident:

*"It appears that Miley didn't learn the lesson last year and hasn't been taking enough care over her password security to avoid the same fate, other users should make sure they choose strong passwords that can't be easily cracked, and Twitter itself should play a key part in enforcing this."*

*“… I started wondering how vulnerable other sites might be to this type of attack.  … I went looking at some of the sites that I frequent and found that many of them don’t have any restrictions on authentication attempts…*

*And how hard would it really be to create such a script to attempt a brute force attack like the one that was used by the hacker?  Well… How about four simple lines of code attached to a very large dictionary database:”*

```
Set WinHttpReg = CreateObject("WinHttp.WinHttpRequest.5.1")
WinHttpReq.Open "POST","http://domain.com/login",false
WinHttpReq.SetRequestHeader "Content-Type","application/x-www-form-urlencoded"
WinHttpReq.Send("login=Chris&password=Pa$$w0rd")
```

*“I tested this script against a site that I frequent, and it worked as expected.  So, I guess it’s not that hard to perform such an attack.  Now it seems the question isn’t how did this happen to Twitter, but why doesn’t this happen every day?”*

#### Example security issue helped by GPO

A particular problem is the need to disable USB sticks and other removable media in secure installations. You can set up custom .admx files to include this, and apply them via GPO to a group of workstations. This disables various drivers, and generally works a lot better than gluing up the USB ports.

Windows includes extensions to GPs to make this easier such as *Removable Storage Management* but also includes approx. 800 other new policy settings