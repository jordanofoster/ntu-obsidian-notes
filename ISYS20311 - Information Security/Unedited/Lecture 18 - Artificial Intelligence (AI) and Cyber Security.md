#isys20311-infosec/lecture-18
# Artificial Intelligence (AI) and Cyber Security

Cyber security is the main focus of companies in recent years. Providing security is a monotonous and repetitive job, however; we can use the power of machine learning and other data mining techniques to streamline the process.

## Cyber Security

Elements of Cyber Security include:
- Application Security
- Information Security
- Network Security
- Disaster Recovery / business continuity
- Operational Security
- End-user education

Types of Cyber Security Threats include:
- Ransomware
- Malware
- Social Engineering
- Phishing

## Branches of Artificial Intelligence
- Machine Learning
	- These give computers the potential to learn without explicit programming.
- Neural Networks
	- These are a set of algorithms that make use of neurology to imitate the human brain's operating process.
- Robotics
	- This is a field of science that combines mechanical engineering, electrical engineering, computer science, etc., to deploy robots for laborious tasks.
- Expert Systems
	- These are computer systems that mimic the decision-making intelligence of a human expert.
- Fuzzy Logic
	- These are techniques that represent and modify uncertain information by measuring the degree to which a hypothesis is correct.
- Natural Language Processing
	- This helps in communications between computers and humans, through the use of natural language.

### Machine Learning

Computer programs are said to learn from experience $(E)$ with respect to some class of tasks $(T)$, and performance measure $(P)$ - if the performance at $T$ (if measured by $P$) improves with $E$.

Machine learning algorithms generate models from data; there are two types - supervised and unsupervised. Algorithms themselves tend to perform classification and clustering with the assistance of probability, statistics and other fields of mathematics.

![[Pasted image 20220221153614.png]]

#### Machine Learning Algorithms

##### Time-Based Inductive Machines
These are much like the Bayes Network, using probability and a direct graph to predict the nxt event.

##### Instance-Based Learning
These define a distance to measure the similarity between feature vectors.

##### Neural Networks
These can be trained to predict an attack occuring, much like a well-trained human.

#### Classification

This is a form of supervised learning. The class will be predetermined in the ML training phase. The character of classes themselves are also determined during this phase, and it is a common approach in a pattern recognition system.

Classification algorithms include:
- SVM
- Naïve Bayesian Filtering
- Decision Trees
- Random forests
- Logistic regression

Additionally, esembles of 3 algorithms can be present (with voting).

##### Pattern Discovery (from rules)

Existing rules are derived from expert knowledge, or another system. Different methods can measure different aspects of a class (such as intrusions in the [[Lecture 18 - Artificial Intelligence (AI) and Cyber Security#Case Study - Intrusion Detection using Machine Learning|case study.]]) Combination of rules may find other, new patterns (such as unknown attack types). For example:

- Snort has a set of rules that is derived from different persons. These rules may have different aspects of intrusions.
- We can use the data mining or machine learning method to discover the pattern from these given rules.

![[Pasted image 20220221161248.png]]

#### Clustering
Clustering algorithms include:
- K-Means
- Farthest first

##### Limitation of Clustering
Clustering is subjective:


![[Pasted image 20220221154506.png]]


#### Evaluation of Machine Learning Algorithms
![[Pasted image 20220221154048.png]]

This is done through three equations, where:
$tp =$ *true positive*
$fp =$ *false positive*
$fn =$ *false negative*
$$Precision = \frac{tp}{tp+fp}$$
$$Recall = \frac{tp}{tp+fn}$$
$$F1 = \frac{2\times(Precision\times Recall)}{(Precision + Recall)}$$
#### Supervised Machine Learning

An example of supervised learning involves the use of decision trees to distinguish between spam and non-spam email based on the frequency of terms/words, used in a large historical set of phishing and non-phishing emails.

#### Unsupervised Machine Learning

An example of this would include using self-organizing maps and clustering techniques to identify anomalous IP traffic.

#### Reinforcement Learning

This is the training of machine learning models to make a sequence of decisions in a game-like situation, such as bringing threat intelligence and the end user into the loop.

### Benefits of Machine Learning in Cyber Security
Machine learning can be useful in the following Cyber Security contexts:
- Handling large volumes of data
- Security task automation, such as:
	- Malware analysis
	- Network log analysis
	- Vulnerability assessments
	- Raising alarms, etc.
- Threat detection and classification
- Network risk scoring
	- This is the use of quantitative measures to assign risk scores to sections of networks, and helps organisations to prioritise resources.

Also see *Machine Learning and Deep Learning Methods for Cybersecurity*, Xin, Y., et al., 2018  and  *Survey of machine learning techniques for malware analysis*, Daniele U., Leonardo A., & Roberto B., 2022.

#### Application of machine learning in Cyber Security
##### Machine learning for network protection

This can be used for both Intrusion Detection Systems (IDSs) and for network traffic analysis. Examples include:

- Regression, to predict the network packet parameters and compare them with the normal ones
- Classification to identify different classes of network attacks such as scanning and spoofing
- Clustering for forensic analysis

##### Machine learning for application security

Web Application Firewalls (WAFs) can have some help from machine learning, but a universal model cannot be developed to deal with all threats; some examples are listed below, however:

- Regression to detect anomalies in HTTP requests, such as auth bypass.
- Classification to detect known types of attacks, such as injections (SQLi, XSS, etc.)
- Clustering of user activity, to detect DDOS attacks and mass exploitation.

##### Machine learning for user behaviour

Unlike malware detection (which focuses on common attacks), user behaviour is a complex layer and an unsupervised learning problem, which cannot be easily solved through training of a classifier. Examples include:

- Regression to detect anomalies in user actions (such as logins at an unusual time)
- Classification to group different users (for peer-group analysis)

## Cyber Security Tasks
1) Prediction
2) Prevention
3) Detection
4) Response
5) Monitoring

## Case Study - Intrusion Detection using Machine Learning

### Background

An intrusion can be identified as any set of actions that attempt to compromise the CIA triad of a resource. There are three classes of intruder:
- The masquerader, an illegitimate user that penetrates the system using a legitimate user's account
- The misfeasor, a legitimate user that misuses his/her privileges by accessing resources that are not authorised.
- The clandestine user, a privileged user that uses their supervisory control to suppress audit control.

Intrusions themselves are the activites that violate the security policy of the system, and Intrusion Detection is the process to identify them.

### Structure of an IDS

![[Pasted image 20220221160112.png]]

### Types of IDS

#### Host-based IDSs

These get audit data from host audit trails, and detect attacks against a single host.

#### Distributed IDSs

These gather audit data from multiple hosts, and possibly the network that connects them. They are designed to detect attacks that involve multiple hosts.

#### Network-Based IDSs

These use network traffic as the audit data source, relieving the burden on the hosts that usually provide normal computing services. These are designed to detect attacks from the network.

### Intrusion Detection Techniques

#### Association Rule Mining (Pattern Discovery)

The goal of this technique is to derive multi-feature (attribute) correlations from a set of records. An example of an expression of an association pattern is as follows:
![[Pasted image 20220221160710.png]]

#### The Machine Learning Methods







