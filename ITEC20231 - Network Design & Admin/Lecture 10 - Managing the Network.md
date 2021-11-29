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
- 