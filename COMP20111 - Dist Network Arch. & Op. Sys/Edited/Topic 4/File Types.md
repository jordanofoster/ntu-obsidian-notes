#comp20111-dnaos/topic-4 
# File Types

- Most OSs support several filetypes:
	- **Regular**
		- Ordinary files that contain data
			- For example, archival file:
			>![[ExampleArchiveLayout.png]]
	- **Executables**
		- [[Programs|Program code]] executable by OS:
		>![[ExampleExecutableLayout.png]]
	- **Directory/Folder** ^e4c368
		- System files that *reference other filetypes*
	- **Special Characters**
		- Not true files; directories that refer to *character devices*
			- Allows communication with I/O devices
	- **Block Special**
		- Not true files; directories that refer to *block devices*
			- Allows communication with *storage devices*
				- Such as [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disks]] or [[Volatile Memory#Random Access Memory RAM|main memory]]
