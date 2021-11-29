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

There can be lots of GPOs within a domain; the Group Policy Management Console provides you with a way to manage these GPOs,
