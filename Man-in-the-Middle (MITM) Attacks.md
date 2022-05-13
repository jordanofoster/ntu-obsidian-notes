#isys20311-infosec/lecture-3 
# Man-in-the-Middle (MITM) Attacks

- An attacker secretly *monitors* and sometimes *alters* transmissions between two parties
	- Variety of techniques:
		- [Packet sniffing](https://en.wikipedia.org/wiki/Packet_analyzer)
			- Monitoring/viewing packets sent between parties
		- [DNS hijacking](https://en.wikipedia.org/wiki/DNS_hijacking)
			- Redirect domain requests to IPs of *malicious webservers*
				- Instead of intended site
		- [Session hijacking](https://en.wikipedia.org/wiki/Session_hijacking) ^2e3d1e
			- Take session tokens from *previous login* to make requests as a specific user