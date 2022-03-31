# Taking the Network Outside of the Workplace
Networks are moved outside of the workplace under the following circumstances:
- Laptops are used outside of the office
- Web access to your services
- Data storage devices/media are taken outside of the office
- Printed material is taken home.
- (Special case) access to a wireless network from outside of the building.

## What are the Issues?
Mainly, Security - particularly because in such circumstances, users believe that they are doing nothing wrong; indeed, in some cases, taking the network "outside" may be necessary for their job.

## An Important Reminder
*All* security can be breached, given enough time and money, and this is represented by how devices are advertised:
- *Encrypting PIN Pad Devices* specify attack resistance in terms of cost and time required.
- Safes use a *UL* (Underwriters' Laboratories) rating system (e.g., TL-15, TRTL-30, etc.)

On many occasions, security conflicts with ease, convenience and productivity; technical security measures must be supported by physical and "intellectual" security (resistance against social engineering).

## Use of a work laptop outside
- Files can be held in the following manners:
	- On a local drive
	- On a server, available offline via caching.
- Email (accessed via web browser)
- Other potential data vectors.

### Files held on a Local Drive
These are vulnerable if the laptop dies anyway, so the user must be educated about backups. We must also consider what happens if the laptop gets stolen:
- We ensure the non-domain account also has a decent password/other protection (by, again, educating the user)
- Encryption must also be considered:
	- Are the files worth protecting?
	- If so, which files?
- Some files may only be worth *recovering*
	- This means they would cost time/money to restore, but do not contain sensitive information in and of themselves.

### Files from Servers
Some users may want local copies to work on while offsite, meaning that they would need file caching to be turned on. If the laptop is stolen, such files are now at the same level of risk as locally stored files; even if security is not an issue, the work is lost.

The best solution to security in this instance may just be encryption.

### Email via the web browser
There are several issues that may occur here; the contact list/address book may need to be secured, and attached files may remain in the browser cache. It should also be noted that users of web email in open-access machines (such as those in airports) are liable to leave the machine without properly logging off.

### Other Laptop Issues
- What happens if the laptop is shut; does it lock the desktop or just hibernate?
	- You must ensure secure settings.
- Are users educated about using machines on public transport (where data is visible to shoulder-surfers)?
- Are all laptops fully up-to-date, and with their own firewall, etc., in-case free Wi-Fi is used?
- Consider switching off [*everything*](http://www.theregister.co.uk/2007/08/01/defcon_survival_guide/) when in vulnerable locations.

## Encrypting File System (EFS)

![[Pasted image 20220331193742.png]]

If the admin removes/resets the password from a user account, all EFS encrypted files, personal certificates and stored passwords are lost. This does *not* happen if a user does a password change.

As a result, it is *extremely* important that at least *one* recovery agent (preferably more) exists. The domain administrator is the default recovery agent:
- They can use group policy to explicitly designate recovery agents.
	- If a user loses their key/resets password/leaves company, the recovery agent can access the files, decrypt them and even remove encryption entirely (if required).
	- Agents cannot impersonate a user; they can only decrypt files.

### How to use EFS?
![[Pasted image 20220331211056.png]]
The recommended method is as follows:
- Create an NTFS folder, then use *Properties -> General -> Advanced...* to select encryption. Only the files within the folder are encrypted; the folder itself is not.

### EFS and its interactions with NTFS
Moving or copying a file into an encrypted folder encrypts the file itself; moving an already encrypted file to an unencrypted folder, however, *does not* decrypt it.

Copying or moving an encrypted file to *another file system* such as FAT32 *does* decrypt the file.
Moving or copying a file, therefore, requires the permission to decrypt.

Files can be backed up in an encrypted state; meaning we need to keep our keys for a long time.

### EFS Best Practices
- Users and recovery agents should export keys/certificates to removable media such as USB sticks.
	- These keys should be stored securely, away from the computer.
- Recovery keys are important, because they can be designated for a large number of users.
- Users should encrypt folders, rather than files.
- A well-organised procedure should be in place for any change of recovery agents.
	- Keep keys until all files that *might* have been encrypted with them are re-encrypted with new keys.

### Further Protections for EFS
SYSKEY is enabled by default to randomly hide the system master key within the registry. This method protects the SAM database, alongside other important details, but this obfuscation method has been [cracked](http://www.irongeek.com/i.php?page=security/localsamcrack2) - it is thus recommended to switch from SYSKEY to password mode, as this never leaves the key available on the machine.

![[Pasted image 20220331212544.png]]

EFS does not defend against those who can demand or otherwise forcibly extract encryptions keys, such as the government. Therefore, further methods might be necessary for foreign spies, criminal organisations and the paranoid, such as [deniable encryption.](https://en.wikipedia.org/wiki/Deniable_encryption)