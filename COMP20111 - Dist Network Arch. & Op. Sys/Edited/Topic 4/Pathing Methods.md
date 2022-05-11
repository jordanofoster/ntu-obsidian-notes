#comp20111-dnaos/topic-4 
# Pathing Methods

![[Pathing.png]]

There are two common methods:
- **Absolute** ^5ccc9c
	- Relative to *root* directory and *unique*:
		- `/`  in UNIX $\rightarrow$  `/NTU/dnaos/demo.c`
		- `\` in MS-DOS/Windows $\rightarrow$ `\NTU\dnaos\demo.c`
- **Relative**
	- Relative to *current/present working [[Directories and Folders|directory]]*:
		- For example, if current directory is `/NTU/dnaos/`: 
			- A file with [[Pathing Methods#^5ccc9c|absolute path]] `/NTU/dnaos/demo.c` can simply be referred to as `demo.c`
	- Special entries such as `.` and `..` can be used also:
		- `.` $\rightarrow$ *current directory*
			- `cd .`
		- `..` $\rightarrow$ *parent directory*
			- `cd ..`
