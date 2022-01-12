# Encryption
Encryption is used to provide [[ISYS20311 - Information Security/Lecture 1 - Overview#Confidentiality|confidentiality]], integrity, authentication and non-repudiation. It exists in *Symmetric* and *Asymmetric* forms. A basic overview of how it works is shown in the following video, from `1:22-3:50`:

<iframe width="896" height="504" src="https://www.youtube.com/embed/UiJiXNEm-Go" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 Encryption is *important* as a key control in managing risk; as a result, we need to know what it can be applied to, and have a foundational understanding of the technology itself. 
 
 Encryption is also a key requirement for compliance with laws and regulations, and in regards to protecting data subjects, as we need to worry about data at rest and in transit, and verifying identities, transactions and communication.

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

 ## Symmetric Encryption

 With this, the same key is used to both encrypt and decrypt the data. This has a low overhead in terms of resources, but key management is an issue - how is the key *safely* shared between authorised parties?

 Additionally, the number of keys increases exponentially with the number of communicating parties.

 ## Asymmetric Encryption

 Here, two keys with mathematical relations are used; one to encrypt, and one to decrypt. The *public* key (responsible for encryption) is openly distributed for anyone to access, whereas the *private* key (responsible for decryption) is made only available to the keyholder.

 By using the public keys of other parties, data can be encrypted to recipients, who can then *decrypt* the data safely using the associated private key.

 ## Message Integrity

 Digests, Hashes and Checksums produce a *fingerprint* of a message that can be used to verify the message integrity. These are one-way functions, meaning that data is lost in the process (and thus, the message cannot be reconstructed from the hash).

 The receiver can use the same one-way function on a received message, and check the hash they produce to ensure it verifies the hash they receives. This is a way of *verifying* message integrity.

 ![[Pasted image 20220112002244.png]]

 (Need to make notes seperately on this by watching lecture).

## Authentication & Non-Repudiation
This refers to the idea that you can be certain of who you are talking to (*Authentication*), and that they cannot deny having sent a message (*Non-Repudiation*).

Using our private key, we can *sign* a *hash/message digest* to form a *digital signature*. As the private and public key are related, the recipient can then use our *public* key to verify our identity. 

### Digital Signatures (Green Circles)
![[Pasted image 20220112002408.png]]
(Again, notes)

#### Altogether (Integrity, Authenticity, Nonrepudiation and Confidentiality)
![[Pasted image 20220112002440.png]]
(Ditto).

## Man-in-the-Middle Attacks

Malicious third parties can try and get in between two communicating parties, allowing them to substitute their own key into the exchange that *spoofs* the identity of one of the genuine parties.

As a result, mechanisms need to exist to verify keys against this attack vector; this is the job of certificate authorities who sign keys with their *own* private key to prove their origin, and is referred to as Public Key Infrastructure (PKI).

## Popular Encryption Algorithms

### Triple DES

The DES (Data Encryption Standard) was an old standard that used a 56-bit key. Due to the short keylength and comparatively weak primitive, this can be now cracked in hours; despite this, it can still be found occasionally, such as on some smartcards.

*Triple* DES involves running the DES algorithm three times, a process known as [multiple encryption](https://en.wikipedia.org/wiki/Multiple_encryption). This results in a 168-bit encryption output, but has a weakness; if keys 1 and 3 are the same, it is reduced to 112-bit strength.

The algorithm is slow because of the triple run, and uses short block lengths to compensate; regardless, it is being phased out for better algorithms.

