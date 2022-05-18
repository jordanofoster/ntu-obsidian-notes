#isys20311-infosec/lecture-2 
# The Need for Information Security & Threat Overview

## Why is information security needed?

Businesses have **information of value** that must **retain confidentiality,** such as:
- **Intellectual property**
- **Business data**
	- Customer data,
	- Contract information, etc.
- **Personal data  (Staff)**
- **A brand to keep reputable.**

Businesses are **dependant on the information they hold** to exist, relying on proper access to the right information at the right time; and as such, **confidence in integrity** and **availability** are paramount.

### Software, Data, Network & Physical Security

#### Software Security

The following must be considered in regards to software:
- Whether software utilised is **critical to a business objective**
- Whether software is **susceptible to adverse modification**
- Whether software is **susceptible to deletion/removal**

#### Data Security

Data refers to **content stored on databases and other storage** throughout an organisation. It must protect against unauthorised **access and modification,** as well as **prevention of access altogether.** Data is often one of the **most critical assets** to an organisation.

#### Network Security
Network security involves **protection of infrastructure** that is used for business. Problems that are commonly faced in this regard are:

- Denial of access
- Theft of information
- Complexity as an organisation scales
	- Systems are **only as strong as their weakest link.** This is harder to manage in larger systems.

#### Physical Security
Physical security relates to the **physical assets** that faciliate business, such as buildings, machines, servers, etc. These tend to be easier to protect as **remote attackers** are not as much of a consideration.

### The Threat Landscape

Threats have no easily defined origin, and can include many different adversaries:
- Criminals
- Corporate competitors
- Hackers
-  'Hacktivists'
-  Employees

As a result, it is **impossible** to determine the **capabilities and motivations of attackers** - it is best to **reduce opportunity where possible.**

### Types of Attacks

#### Untargeted Attacks

Adversaries using this method typically are **not specifically targeting one asset/company** - they instead use dragnet methods to **catch insecure systems.** Their methods include various methods of social engineering, such as **phishing** and **water holing** (although not meticulously designed), **scanning networks for vulnerabilities** and **deploying ransomware.**

#### Targeted Attacks

Typically the realm of hackers and other specialist adversaries, targeted attacks also make **prominent use of social engineering** with tailor-made attacks such as **spear-phishing,** by sending emails to specific individuals to steal their credentials. They also **make use of botnets,** and will sometimes attempt to **subvert the supply chain** by **damaging key infrastructure.**

#### Insider Threats

Anyone with **legitimate access** can also use that same access to cause harm. This is commonly just **human error,** but can also include **ex- and otherwise disgruntled employees.**

### Threat Vectors

Vectors are the **routes taken to breach a system.** As threats themselves are difficult to define, security efforts are often placed towards **examining exploitable vulnerabilities.** This can involve thinking about various processes, such as:

- How access is gained to/within buildings
- How users interact with front-facing services
- How staff go about their work, and what is required for them to do so.

### Stages of an Attack

Attacks can be defined in four stages, as seen below:

![[AttackChain.png]]

Attackers **survey** the network for vulnerabilities, then proceed to **deliver** malware/tools to **breach** system security and **affect** assets.

## Statistics 

`Actually neccessary? Unknown.`

## Who needs to consider implementing INFOSEC?

Put simply, everyone - any organisation regardless of size **can be a victim of attacks,** as they all **have business critical assets.**

### Barriers to implementing INFOSEC
Some general issues:
- The rapid change in the business world and particularly **increased globalisation of business** presents many new threat vectors.
- Business needs and security requirements tend to be at odds due to the inherent inconvenience security brings.
- Security changes may clash with the culture of an enterprise
- The cost of a solution and its security impact must be balanced accordingly.

#### Negative Attitude

Organizations are prone to a lot of bureaucracy that **limits ideal implementations.** These include:

##### Operational Constraints
- **Slow/limited access to information**
- **Passwords hard to remember**
- **IT Security personnel "Jobsworths"**

##### Financial Constraints

- "Must be expensive"
- "It's for *big* organisations"
- "We aren't a target"
- Organisation is complacent because of **no history of breaches/attacks**

##### Cultural Constraints

- Unpopular with staff members due to inconvenience
- Lack of understanding from those in management
- Ignorance towards the risks that are present

#### Positive changes towards implementation of INFOSEC

Attitudes towards the importance of INFOSEC is gradually improving

##### Risk aversion

- Organisations are beginning to become **more threat aware**
- Organisations and Staff are realising that **breaches can happen to anyone**
- **Contractual obligations** to uphold INFOSEC practices are **more prominent**
- **Regulations and Legislature** are forcing companies to be held accountable for neglectful practices

##### Competitiveness
Getting any advantage possible to remain at (or near) the top is paramount in industry.
- Implementing INFOSEC acts as **supply chain assurance**
- Procurement Qualifier (?)
- Reputation Management (?)

##### Corporate governance
- Corporations have a **responsibility to stakeholders** to **protect their assets**
- Directors have their **own obligations** that require INFOSEC
- Ignorance of INFOSEC practices is no longer an acceptable defence

### Cost-cutting on the part of organisations 

#### Security through Obfuscation

Refers to reliance on hiding design details in an attempt to **protect assets,** in the misguided notion that attackers with little knowledge regarding inner workings or the location of assets can also do little harm, thereby **underestimating their intelligence** in many cases.

It also **broadcasts vulnerability** - showing **you have something to hide** makes it worth more to assailants, particularly hackers, who might view it as **an admittance of insecurity** by the organisation.

Summarily, a **poor choice** for security assurance that adds little to an already strong system at best and is sometimes viewed as  a **substitute for actual security.**

#### Reactive vs Proactive INFOSEC

Many organisations are hesitant to spent money on **proactive INFOSEC** as it guards against things that *might* happen instead of *will* happen. It is also **impossible to completely remove risk** when acting proactively and it is hard to assess what *might* happen and how likely it is. Despite this, **reactive INFOSEC should be deployed** in the event an attack happens so that it **doesn't happen again.**

#### Balancing cost and security benefit

As a general rule, measures taken must **not prevent use** of the asset altogether. Money spent on security also tends to have diminishing returns, and the effective budget to spend on an asset is **no more than the money it is worth** - since there is no point on spending £1000 on a £100 asset.

## Information Assurance
According to the UK Cabinet Office, information assurance is *"The confidence that information systems will protect the information they carry and will function as they need to, when they need to, under the control of legitimate users."* Information systems in this context are **not neccessarily technical** - and assurance is made through a series of policies, programs, documentation and technical implementations organization-wide.



