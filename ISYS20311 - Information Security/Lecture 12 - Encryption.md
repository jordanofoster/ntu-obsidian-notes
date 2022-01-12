# Encryption
Encryption is used to provide [[ISYS20311 - Information Security/Lecture 1 - Overview#Confidentiality|confidentiality]], integrity, authentication and non-repudiation. It exists in *Symmetric* and *Asymmetric* forms. A basic overview of how it works is shown in the following video, from `1:22-3:50`:

<iframe width="896" height="504" src="https://www.youtube.com/embed/UiJiXNEm-Go" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 Encryption is *important* as a key control in managing risk; as a result, we need to know what it can be applied to 
## Simple Ciphers
These are historical [cryptographic primitives](https://en.wikipedia.org/wiki/Cryptographic_primitive) that have mostly been subject to thorough [cryptanalysis](https://en.wikipedia.org/wiki/Cryptanalysis) that renders their modern use ill-advised, but they are mentioned here to form a basic understanding of the concept:

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

Alternatively (and, done right, this is still a strong practice):
- Hiding messages in plain sight ([security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity))
	- [Steganography](https://en.wikipedia.org/wiki/Steganography), word coding and other [COMSEC](https://en.wikipedia.org/wiki/Communications_security) practices

### An example of coding/hiding in plain sight

The following message looks like glowing praise of an employee, read normally:


LETTER OF RECOMMENDATION

*Bob Smith, my assistant programmer, can always be found  
hard at work in his cubicle. Bob works independently, without  
wasting company time talking to colleagues. Bob never  
thinks twice about assisting fellow employees, and he always  
finishes given assignments on time. Often Bob takes extended  
measures to complete his work, sometimes skipping coffee  
breaks. Bob is a dedicated individual who has absolutely no  
vanity in spite of his high accomplishments and profound  
knowledge in his field. I firmly believe that Bob can be  
classed as a high-calibre employee, the type which cannot be  
dispensed with. Consequently, I duly recommend that Bob be  
promoted to executive management, and a proposal will be  
executed as soon as possible.*

Sincerely,
Project Leader

If we only read every second line though, it becomes rather more sinister:

LETTER OF RECOMMENDATION  

**Bob Smith, my assistant programmer, can always be found**  
*hard at work in his cubicle. Bob works independently, without*  
**wasting company time talking to colleagues. Bob never**  
*thinks twice about assisting fellow employees, and he always*  
**finishes given assignments on time. Often Bob takes extended**  
*measures to complete his work, sometimes skipping coffee*  
**breaks. Bob is a dedicated individual who has absolutely no**  
*vanity in spite of his high accomplishments and profound*  
**knowledge in his field. I firmly believe that Bob can be**  
*classed as a high-calibre employee, the type which cannot be*  
**dispensed with. Consequently, I duly recommend that Bob be**  
*promoted to executive management, and a proposal will be*  
**executed as soon as possible.**  

Sincerely,  
Project Leader  
