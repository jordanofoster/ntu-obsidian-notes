# Incident Prevention

In past lectures, we have learned how to write policies to (hopefully) prevent indcidents. Unfortunately, people do not always follow policy, and incidents *do* still happen.

There are three ways to help policies to work:
- [[Lecture 13 - Incident Prevention#Check that staff know the policies|Check that staff know the policies]]
- [[Lecture 13 - Incident Prevention#Check that staff follow the policies|Check that staff follow the policies]]
- [[Lecture 13 - Incident Prevention#Real-Life Scenarios|Real-Life Scenarios]]

In the inevitable outcome that policies eventually *don't* work:

- [[Lecture 13 - Incident Prevention#Training options|Training options]]
- [[Lecture 13 - Incident Prevention#Stick and Carrot|Stick and Carrot]]

### Check that staff know the policies

There are several methods:

- Spot checks - visit someone at their desk and give them a policy quiz

- Host a lunchtime quiz on the policies, with prizes

- Put up big posters to remind people of policies, in order to keep the profile of the policies high

### Check that staff follow the policies

With the spot checks:
- Do staff have confidential information on their desk?
- Has their screen been left unlocked? etc.

Self-phishing:
- Some companies send their own staff phishing emails, then analyse how many give away requested confidential information
- There are [free self-phishing tools](https://resources.infosecinstitute.com/top-9-free-phishing-simulators/#gref), and free managed campaigns (usually by a vendor of a commercial tool)

Alternatively, manufacture an obvious breach of policy and observe how many staff report and/or attempt to fix it.

### Real-Life Scenarios

These are done by penetration testers and white hat hackers.
<iframe width="720" height="405" src="https://www.youtube.com/embed/QMAJ4bVB3EI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
### Training options

- Online courses with additional test
- Lectures/seminars
- Q&A sessions with experts
- Mini-apprenticeships
- Simulations, such as the aforementioned self-phishing

## Stick and Carrot
This can be part of a performance review, which can act as both the *stick* and the *carrot.*

Other methods include:

- Highlighting success stories
	- Highling individuals who have contributed by publishing them on company's internal website
- Naming and shaming
	- Naming is a bad idea - but publishing shameful 
	statistics about a group can work.

## Incident Detection

- [[Lecture 13 - Incident Prevention#Monitoring|Monitoring]]
- [[Lecture 13 - Incident Prevention#Dashboards|Dashboards]]
- [[Lecture 13 - Incident Prevention#Anomaly Detection|Anomaly Detection]]
- [[Lecture 13 - Incident Prevention#Artificial Intelligence|Artificial Intelligence]]

### What to monitor?

#### Outbound website traffic (towards internet)

As a minimum, this should include domain names and URLs. If possible though, this should extend to monitoring the full HTTP header information, as it often provides clues to malicious activity.

This is because initial infection and persistent connections are often made through HTTP(S) traffic and could appear to come from user devices (*the most likely source*) or servers.

#### Email traffic

At minimum, the metadata about what is sent/received should be captured. If possible, both email headers and contents should be monitored - if links are visible, attempts at phishing attacks can be connected.

#### IP connections between network and the Internet

It is useful to capture 5-tuple metadata of the accepted connections at the edge of your network, as this shows any raw connections coming out of it. Interesting traffic would include things like:
- HTTP traffic not going through a proxy server
- Direct malware *command/control* sessions

#### IP connections between zones in OT (Operational Technology) networks

For example, server networks. At minimum, 5-tuple metadata from the critical OT zone boundaries (such as the IT/OT interface) should be captured. Such traffic is likely to contain evidence of an attacker's actions against cyber-physical systems.

#### Host-based activity

A host-based monitoring system can detect unauthorised activity on systems themselves, such as unusual/unauthorised activity by software systems. These might evade typical detection systems based on network interfaces.

### Who, when, where...
