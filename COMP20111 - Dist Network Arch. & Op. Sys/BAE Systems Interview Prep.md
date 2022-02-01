### "Why have you chosen to apply for this position with BAE Systems Applied Intelligence?"

The company's focus on cybersecurity and significant history as a defence contractor immediately stood out to me as somebody attempting to break into the industry - the various physical products you offer to clients also seemed like interesting projects to work on, as I have previously studied embedded systems and radio communications as part of my A-level in electronics; the coursework completed as part of that experience (and since) has lead me to seek out further work within this area.

I have also found through university studies that collaborative work with like-minded individuals and the discussion and the collective decision-making involved with such a process quite engaging, as I find myself learning from my peers, both in the outputs of their work and how they approach the issues we face. In addition, the wide range of frameworks and languages presented in the initial application details came across as an opportunity to expand my skillset alongside current hobbyist projects.

Essay with maximum character length of 1000. 1 attempt, no time limit.

### "Tell us about a time you were given a number of challenging activities to complete within a specific timeline. Please describe your approach, the steps you took, and how you made sure to finish all of the activities correctly and on time."

#### SAD Module (first year)

- Project manager 
	- Had to produce a design document for a COVID-19 test and trace app as part of team of five. 
	- Submission was lengthy enough to require scheduling of work and assignment of plans, and we were provided with 'soft' deadlines for various sections.

- Work sections:
	- Requirements Analysis, 
	- Timeline, 
	- Flowcharts, 
	- UML Diagrams, 
	- UI Design 
	- Conclusion

- 2/3 team members present for almost all of coursework, including myself. 
- Member attendance was inconsistent at times and plans had to be adapted for those present.

- Had to adapt to lower working capabilities:
	- By prioritising work that was most important, working in group calls to ensure productivity
	- Getting work done when people were not present to do it themselves.

- Kept in frequent touch with our module tutor about attendance of others, and frequently sought out feedback on work where possible to ensure efficient use of limited productive resources and that tasks were being done properly.

- Frequently moved from 'managerial' to 'worker' role both to ensure accountability and timely completion of tasks.

**Video question with maximum response time of 180 seconds (3 minutes), and a minimum of 10 seconds.**

**Three attempts. 30 seconds to prepare before each attempt.****

### "Tell us about a time you had to solve a problem at school or at work, but you were given confusing information. Please describe the situation, what you did, and the outcome."

#### Advanced Networking Labs:

- Told to simulate a client-server connection in lab by tutor using Windows 10 guest VMs
- Lab computers configured as part of locked-down LAN, no administrator access on host

- Tutor intended for machines to be connected directly via ethernet using host NIC - did not work due to host configuration, unchangeable due to not having administrator privileges

	- Configuration had to be done manually with peer via troubleshooting, and discussing/debating what the possible issues may be with my peer, knowledgeable with networks due to pentesting as a hobby
	
	- We bypassed the host system's restrictions via USB passthrough with an ethernet adapter, connecting both devices this way instead
	
	- From there after configuring the properties of the adapter on each system to point to the other and disabling restrictions (firewall) we were able to confirm a connection using `ping`
	
- Given server and client python scripts - scripts did not work:
	- Server socket on UDP, client on TCP
	- General code was written under Python 2, but being run on Python 3 interpreter
	- Many other issues that required a full rewrite of the scripts, visually debugging the code as a paired duo due to lack of tools (using Python IDLE)

- Learned a lot about adapting to lack of information/unforseen circumstances, and using our differences in skills to overcome the challenge

- The solutions we came to by troubleshooting the lab and rewriting the scripts provided were later used by the lab tutor to update the instructions and code to be similar to our outcome.

Video question with same response lengths as prior. Same number of attempts and same amount of prep time.

### "Please describe a time you were asked to perform skills or meet requirements that were outside of your comfort zone. Describe the situation, the steps you took, and the outcome."

#### Tomorrow (C++ Graphical Calculator)
- Working on C++ graphical calculator project (tomorrow) with friend made during Derby University game development workshop.
- No prior experience with the C family of language at the time - only had experience with Visual Basic, .NET, and Python
	- First time experiencing class constructors, strong typing/strict syntax, no namespaces being normally imported (unlike python) and compile-time evaluation through constexpr, alongside general compiled languages.
	- Shadowed peer during his work on the project by pair programming and would ask/receive questions regarding the code being worked on to learn, as well as familiarising myself with the concepts through reading documentation
	
- Became a lot more familiar with the C family of languages through this process, and as one of my first experiences working on a hobby project, showed me a lot of the issues that can arise through collaboration (issues with building on different systems as I used Visual Studio and he used CMake on Ubuntu).

Video question. Ditto.

### "A snail climbs on a wall, it starts at the bottom and climbs up $n$ meters a day. Regretfully, every night it slides $m$ meters down. Given the height of the wall $H$, write a program to calculate how many days required for the snail to reach the top of the wall."

"Easy" programming challenge. Markdown enabled.

Input: *"Three non-negative integers $n$, $m$, and $H$ separated by a space. For example:*

```
3
2
11
```

Four samples are given. The following languages are permitted:

- Bash
- C
- C# 8
- C++
- Clojure
- Go
- Haskell
- Java
- JavaScript
- Kotlin
- Objective-C
- OCaml
- Perl
- PHP
- Python 2
- Python 3
- R 3
- Ruby
- Scala 2
- Swift

Output: *A single integer number, which is the number of days required for the snail to reach the top of the wall. For example:*

```
9
```
***If the snail will never be able to reach the top of the wall, print "Fail".***

Four samples are given.

```
from math import ceil


class InputNumException(Exception):

    # Just defining this to make a later try-except statement cleaner.
    # Possibly overkill, and typically would be in a separate module.
    pass


# Main function to calculate days to climb.
def daysToClimb(climbMeters, fallMeters, wallHeight):

    netGain = climbMeters - fallMeters
    if netGain <= 0:
        return "Fail"
    else:
        # We use math.ceil to round up - integer output required
        # We use '/' instead of '//' to avoid floor division...
        # ...and give us an accurate float to work with

        daysToClimb = ceil(wallHeight/netGain)
        return daysToClimb


# Function to extract needed variables from our input string.
def extractVals(inputString):

    intList = []
    for char in inputString.split():
        # If our character is an integer and not negative:
        if char.isdigit() and not(int(char) < 0):
            intList.append(int(char))
    return intList


# Our main program function that ties everything together
def main():

    try:

        parsedInt = extractVals(input("Put your values here:\n"))
        if len(parsedInt) != 3:
            raise InputNumException("Less/More than 3 inputs provided.")

    except InputNumException as e:

        print(str(e) + "\nExiting...")
        quit()

    except Exception as e:

        print("Unknown error. Dumping traceback:\n" + str(e) + "\nExiting...")
        quit()

    else:

        # Climb distance, fall distance and wall height respectively
        outcome = daysToClimb(parsedInt[0], parsedInt[1], parsedInt[2])
        print(outcome)


main()

```
[C:\Users\Jordan Foster\Documents\Project Scratchpad\test.py](file:///C:/Users/Jordan%20Foster/Documents/Project%20Scratchpad/test.py)
### Three personality/cognitive tests - Shapedance, Numerosity, Portrait

2 Retries permitted. 30 seconds to prepare before each game.