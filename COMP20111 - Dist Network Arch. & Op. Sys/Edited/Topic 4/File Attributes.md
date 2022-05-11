#comp20111-dnaos/topic-4 
# [File Attributes](https://en.wikipedia.org/wiki/File_attribute)

These are a type of metadata that describe or affect how [[Files|files]]/[[Directories and Folders|directories]] behave. An example table is listed below:

| Attribute | Meaning |
| --------- | ------- |
| Protection | Who can access the file and in what way |
| Password | Password needed to access the file |
| Creator | ID of the person who created the file |
| Owner | Current owner |
| Read-only flag | `0` for read/write; `1` for read only |
| Hidden flag | `0` for normal; `1` for do not display in listings |
| System flag | `0` for normal files; `1` for system files |
| Archive flag | `0` for has been backed up; `1` for needs to be backed up |
| ASCII/binary flag | `0` for ASCII file; `1` for binary file |
| Random access flag | `0` for sequential access only; `1` for random access |
| Temporary flag | `0` for normal; `1` for delete file on process exit |
| Lock flags | `0` for unlocked; non-zero for locked |
| Record length | Number of bytes in a record |
| Key position | Offset of the key within each record |
| Key length | Number of bytes in the key field |
