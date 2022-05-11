#comp20111-dnaos/topic-4 
# Directory Operations

OSs provide the following syscalls:

- **Create**
	- Empty directory is created
- **Delete**
	- Existing directory can be deleted
		- May be blocked, depending on if it's empty or not
- **Opendir** ^90af86
	- Directory can be read
		- e.g. to list all files in directory
- **Closedir**
	- Directories should be closed after reading, to free space
- **Readdir**
	- Next entry in [[Directory Operations#^90af86|open directory]]
- **Rename**
	- Same method as with [[File Operations#^ac5401|files]]
- **Link**
	- Allows files to appear in *more than one directory*
- **Unlink**
	- Unlinked files are only present in *one* directory

More specific syscalls exist depending on OS.