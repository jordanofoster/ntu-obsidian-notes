# Encryption

## Simple Ciphers
These are historical [cryptographic primitives](https://en.wikipedia.org/wiki/Cryptographic_primitive) that have been subject to thorough [cryptanalysis](https://en.wikipedia.org/wiki/Cryptanalysis) that renders their modern use ill-advised, but they are mentioned here to form a basic understanding of the concept:

- Caesar Cipher
	- Shift all letters in the message by 3 positions in the alphabet
- Rot-13
	- Shift all letters in the message by 13 positions in the alphabet
		- Used in early Unix systems
- St Cyr cipher
	- Shift all letters in the message by $x$ positions in the alphabet
- Vigenere cipher
	- This is a rotating St Cyr cipher based on the letters of a keyword.
		- For example, using keyword *CAB:*
			- Shift the letters by 3(C), 1(A), 2(B), 3(C), 1(A), 2(B)...
- Hiding messages in plain sight ([[Lecture 3 - Cyber Attacks#]])
	- [Steganography](https://en.wikipedia.org/wiki/Steganography) 