# Voice over IP (VoIP) and Session Initiation Protocol (SIP)

## The Information Concept

![[Pasted image 20220131150427.png]]

It is not the *actual* message, but the likelihood of a message that relates to information - the more likely a message, the lower the information. For example:

![[Pasted image 20220131150508.png]]

Therefore, the relationship between Information and the Probability of Information $=(probability)^-1$

Can we measure information? We need a function such that:
- It is inversely proportional to probability, $P(likelihood)$.
- If we have two information, the information, $i$, adds.

This is the case if $I = \log (\frac{1}{p})$
But actually, $I = \log_{2}(\frac{1}{p})$ - The information has a pseudo-unit - the BIT.

Now to measure information, all we need to know is the probability or likelihood of a message.

Another example: what is the information in being told the card picked from a deck of playing cards?

Calculators don't typically know how to do \log_{2}, so we need to help them:

$\log_{2}X = \frac{\log_{10}X}{\log_{10}(2)} = 3.32\log_{10}X$, where $X = \frac{1}{\frac{1}{52}} = 52$

For reference, $\log_{10}$ is the default base of $\log$ when using a calculator.

### Entropy

#### The average information per message

Message sources usually have more than one message:

$I_1 = \log_{2}(\frac{1}{p_1})$, $I_2 = \log_{2}(\frac{1}{p_2})$, etc.

To get the average, multiply the information by the likelihood of the message and add them together. Given a special name Entropy, $H$:

$H = p_1I_1 + p_2I_2 + .. = p_1 \log_{2}(\frac{1}{p_1}) + p_2 \log_{2}(\frac{1}{p_2}) + ...$

$H = \sum_{k}p_kI_k = \sum_{k}p_{k}\log_{2}(\frac{1}{p_{k}})$

for reference, $\sum$ means to sum over all values of $k$.

#### Entropy Example

Entropy of a message source in a table:

| Message | Probability, $p$ | $I$ | $p \times I$ |
| --- | --- | --- | --- |
| A | 0.4 | 1.32 | 0.53 |
| B | | | |
| C | | | |
| D | | | |

## VoIP

### The Concept

- There is an increasing trend towards networks consisting entirely of IP-based devices.
- Internet is typically cheaper than the typical telco's PTSN systems



