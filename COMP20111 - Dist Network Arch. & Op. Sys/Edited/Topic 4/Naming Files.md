#comp20111-dnaos/topic-4 
# Naming [[Files]]

- Done so that user doesn't need *numerical addresses*
	- Different OSs enforce different filename conventions
		- Some common patterns:
			- $\text{char length} \leq 260$ - Windows/UNIX
			- Character restrictions:
				- `?` invalid in Windows, valid in UNIX
			- Case sensitivity:
				- UNIX is
				- Windows isn't

 ![[FileBasenameExtension.png]]

- **Extensions** tell OS/user the *type* of data stored:
	- For MS-DOS, no longer than 3 characters
	- UNIX doesn't care (user choice)
		- Doesn't enforce extensions itself
			- Programs do instead - e.g. C compiler wants `.c` files
- OSs with GUIs associate extensions with *[[Programs|applications]]*
	- E.g. Word opens `.docx` files
	- Prevents security issues:
		- Easy to modify/corrupt files by changing extension
		- OSX prevents this by determining type through contents

## Table of Commonly Used File Extensions

| Extension | Meaning |
| --------- | ------- |
| `file.bak` | Backup file |
| `file.c` | C source program |
| `file.gif` | Graphical Interchange Format image |
| `file.html` | Word Wide Web HyperText Markup Language document |
| `file.iso` | ISO image of a CD-ROM (for burning to CD) |
| `file.jpg` | Still picture encoded with the JPEG standard |
| `file.mp3` | Music encoded in MPEG layer 3 audio format |
| `file.o` | Object file (compiler output, not yet linked) |
| `file.pdf` | Portable Document Format file |
| `file.ps` | PostScript file |
| `file.tex` | Input for the TEX formatting program |
| `file.txt` | General text file |
| `file.zip` | Compressed archive |