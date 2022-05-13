#isys20311-infosec/lecture-3 
# Denial of Service (DoS) Attacks

- Make an asset *unavailable* to authorised users/[[Processes|processes]]
	- Catch-all term for many types of attack, e.g.:
		- [SYN Floods](https://en.wikipedia.org/wiki/SYN_flood) 
			- Exploiting TCP handshakes
		- [Smurf Attacks](https://en.wikipedia.org/wiki/Smurf_attack)  
			- Broadcasting lots of packets using victim's spoofed IP
		- [DDoS Attacks](https://en.wikipedia.org/wiki/Denial-of-service_attack#Distributed_attack)
			- Botnets to carry out large-scale attacks with several *unique IPs* 
		- Malformed Packets
			- Exploiting protocol implementation [[Vulnerabilities]]
				- [Ping of Death](https://en.wikipedia.org/wiki/Ping_of_death)
- Most are *difficult to defend against* - *brute-force* infrastructural sabotage