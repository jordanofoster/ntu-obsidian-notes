# Naming and Structuring Objects

## Objects in a Domain

**Leaf objects** are those at the lowest level in the ADDS; the most important of which being **Computers** and **Users.** Both Computer and User Accounts are necessary to allow a user on a computer to access a resource.

**Groups** are a way of organising computers or users to give all members the same permissions and/or rights. **Organisational Units** primarily exist to allow an admin job to be delegated to separate groups, for example at different physical sites.

### Object Naming

This requires planning, and must be considered for all names within a network, such as the namespaces used for workstations, the servers, users, groups, printers, etc.

Different companies have different policies for this which often reflect their local attitude; the larger an organisation, the better documented their naming policies must be.

#### Namespace Limitations

There are several types of limitations; a **flat namespace** means that names must be unique (e.g. Unix UIDs). **Tree-based namespaces** mean that the same name can be reused on different branches, and this may be useful for simialr organisational structures, such as sales, marketing and accounts names for a company's offices in various different cities.

#### Naming Methods

Various things must be considered when naming resources on a network, such as those that are/are not permitted, how names themselves are selected, how collisions are resolved, and when renaming a resource is allowed. There are several methods:

- Formulaic, for example all NTU logins follow the format N123456
- Descriptive, which include facts - at NTU:
	- Lab machines follow the format of `<Building><Room>_<PCNum>`
		- Such as `MAE205_13`
	- Printers are `<Server>_<Location>_<Type>`
		- Such as `Panhard_MAE2nd_Konica_Col`
	- Functional, which specify roles or duties, such as `admin` or `webserver01`
	- Thematic, such as `homer`, `marge`, `bart`, `lisa` and `maggie`
	- Sometimes no method is used - this results from changes from thematic methods.

##### Difficulties with Naming

- Thematic names are obscure; sometimes it is difficult to remember which functions are hosted on which server.
	- They are also potentially insecure - if admins give standard machines boring names, but name their own machines thematically, intruders will know which are of interest.
- Formulaic names - if users report a fault, will an admin need to be informed of which workstation is bheing used?
- Descriptive names can have unwanted longevity:
	- Names may end up lasting long after the information of use in them is gone, such as defunct departments being included.

## User Accounts

The distinction between *local* and *domain* user accounts must be noted:
- **Local accounts** grant users access to that computer only, and are used for Workgroups.
- **Domain accounts** grant users access to resources across that domain.
- **Domain user accounts** consist of a logon name, password and Security Identifier (SID).

SIDs are used to generate security tokens for resource access. Usernames should be sensible, following company policy, and methods for resolving problems should be present (i.e. dealing with duplicates/lengthy names).

### Creating User Accounts

This must be done by a member of one of these three groups, or those with delegated permissions:

- Enterprise Admins
- Domain Admins
- Account Operators

This should really be done after an Organisational Unit has been created for user accounts - but user accounts can be moved between containers. The simplest method for creating just one new user is to select the OU, then go Action -> New -> User or click the *Create New User* button.

There are 2 pages of information to configure, but the account at this stage can be disabled for use as a template or placeholder for staff arriving at a later date.

![[CreateUsrAccEx1.png]]
![[CreateUsrAccEx2.png]]

#### Creating User Accounts via a CSV File

Multiple users can be added by using `csvde.exe` (CSV Directory Exchange) to import accounts from a file:

1. First, create a CSV file of the user info to be imported.
2. Use `csvde.exe` to import into ADDS.

Syntax:
- Input into ADDS: `csvde -i -f <input file name> -k`
- Dump ADDS database to CSV: `csvde -f <output file name>`

File format example:
```
objectClass, sAMAcctName, dn
user, KentC, "CN=Clark Kent, OU=reporters, DC=DailyPlanet, DC=com"
user, LaneL, "CN=Lois Lane, OU=reporters, DC=DailyPlanet, DC=com"
```

#### Creating User Account using Powershell

Future lectures will cover PowerShell in more detail, but for now, we can use an existing CLI tool, `dsadd`, in a script:

Syntax:
- `dsadd <user> <userDN> [parameters]`
- For example:
	- `dasdd user "cn=Clark Kent, OU=reporters, DC=dailyplanet, DC=com" -ln Kent -fn clark -upn clark.kent@dailyplanet.com`

Alternatively, use a Powershell cmdlet.
- Syntax: `new-aduser <user name> [parameters]`
Example:
- `new-aduser "Clark Kent"`

##### Creating User Templates

Object templates can be used to base newly created objects on:
1. First, setup a template and set all relevant details.
	- This can either be for an existing account, or one specifically for copying (but not a special account type).
2. Ensure the template's password has been set, and the account disabled.
3. To create a new user account based on this template:
	- Action -> Copy brings up a new wizard.
	- This copies some of the user account's properties, but not the User Login name.
	- This new account has a new SID.


## Naming Policies

They should be sensible, documented and frequently used. Easily guessable names make email easier to use (for example, using login names for email), and policies should outline standard procedures for resolving problems, alongside standard schemes (e.g. `FirstName.LastName` or `InitialFirstName.LastName`.

## Passwords

Strong passwords make it harder for hackers to breach an account by increasing time to crack them; but this does not avoid the need for other security measures. Bruce Schnier recommends very strong passwrds, written down and kept inside your wallet - but this is from a post in 2005, and better solutions likely exist these days.

Password policies in AD include **Complexity Requirements**, **Minimum/Maximum Password Age** and **Password History.** The default setting in AD for a new user is to require them to change their password upon next login.

### Security of Passwords

Users must understand the consequences of having bad passwords, by providing them with procedures and documentation. Admins should be aware that encrypted passwords stored on a system are liable to brute force attacks, such as dictionary attacks.

In ADDS, the Lan Manager Hash (LMHash) storage option should be disabled by default as password encryption is very weak and thus easy to crack. Its only modern use is for backwards compatibility with Windows 95/98 and Macintosh.

Linux systems should hide the encrypted password using the etc/shadow file, readable only by the superuser. This is because MD5, the default hashing method, is easily cracked.

## Domain User Accounts

![[DomainUsrAccs.png]]

It is generally good practice for the administrator account to only be used for procedures that actually require its power - sysadmins should have their own unprivileged account for doing most things.

## Groups
Groups are used to ease the burden of administering resources to users; by clustering them based on shared needs, work can be reduced, clarified and made less error prone - for example, if a sales department contains 15 people, there is a significant difference in admin workload if they all need access to 5 resources, depending on whether groups are applied or not (as seen below):

![[GroupsEx1.png]]

### Active Directory Groups

Groups and Group Policies are not directly related; but a Group Policy *can* affect a Group. This is covered further in later sessions.

Groups are not restricted by the structure of the ADDS tree, and generally are used to cluster resources and users.

#### Creating New Groups

Groups can be maintained much like users using the **Active Directory Users and Computers** snap-in. Adding new groups requires elevated rights:
- Enterprise Admins
- Domain Admins
- Account Operators
- Others explicitly granted the right

Once a group has been created, new members can be added via the properties dialogue, or via PowerShell - for example:

`New-ADGroup <group name> -groupscope domainlocal | global | unikversal`
e.g. `New-ADGroup "copyeditors" -groupscope global`

## Computer Objects

These are a **logical representation of a physical object** within ADDS. They authorise that physical device as a **legitimate member of  a domain,** and have a name, location and **who is allowed to manage it.**

COs inherit group policy settings from their containers (e.g. domain/site/OU). During user login, the computer object interacts with the DC to check the domain, if OK'd, then user auth occurs.

### Adding a Computer to a Domain

1. First, create the computer object in ADDS.
2. Join the computer to the domain.
	- The CO can be created as part of the domain-joining process.
3. To create a CO, user must have appropriate perms for the container in which the object will be located:
	- Admins can create objects anywhere in the domain; Account Operators can create objects in the Computers container, and within OUs they create.

### Creating Computer Objects

This can be done using the Active Directory Users and Computers console:
![[CreateCompObjsADUnCc.png]]

Or via a PowerShell cmdlet (`New-ADComputer`):

Syntax: `New-ADComputer <computer name>`
Example: `New-ADComputer "webserver1"`
![[CreateCompObjPShCMDlet.png]]

This method inserts the new computer into the *Computers* container by default.

### Joining Computers to a Domain

![[JoinComp2Domain.png]]

Use system -> accounts setttings, click connect and assign to the domain. Must occur at the computer, and be performed by local admin group member.
