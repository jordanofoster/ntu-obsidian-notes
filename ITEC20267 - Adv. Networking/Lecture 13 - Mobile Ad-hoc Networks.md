# Mobile Ad-hoc Networks

MANETs are defined as a collection of wireless mobile hosts forming a temporary network without the aid of any centralized administration or standard support services. Ad-hoc network terminology itself is dynamic; nodes enter and leave the network continuously.

There is no centralized control or fixed infrastructure to support network configuration, be it initial or revisionary. Example scenarios for MANETs include:
- Meetings
- Emergency or disaster relief situations
- Millitary communications
- Wearable computers
- Sensor networks

## Route Finding

When creating MANETs, we want to determine an optimal way to find the optimal networking routes. There are dynamic links between nodes in MANETs:
- Broken links must be updated when one node moves out of communication range with another
- New links must be formed when a node moves into communication range with another node
- Based on this new information, routes must be modified.

As such, the frequency of route changes are a function of node mobility.

