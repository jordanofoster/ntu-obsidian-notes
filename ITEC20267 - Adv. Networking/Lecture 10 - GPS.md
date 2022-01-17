# GPS

## Coordinate Systems
There are two coordinate systems within GPS; Geographic coordinate systems and Map projections.

### Geographic

These use decimal degrees, measured from the earth's centre to a point on the earth's surface. Points are referenced by longitude and latitude in this manner, and (rarely) altitude is included.
	![[Pasted image 20220117153255.png]] 
	Most satellite devices operate this coordinate system.

### Map Projections

These use mathematical formulas to relate spherical coordinates (on the globe) to a flat, planar format. Different projections can cause different types of distortions; some are designed to minimize the distortion of one or two of the data's characteristics. Projections can maintain the area of a feature, but alter its shape. In the image below, it can be seen that data near the poles is stretched:

![[Pasted image 20220117160906.png]]


## GPS Locating

The locating process works on the basis of an approach called triangulation, which works on the precise time measurements for a signal received from multiple satellites. The steps are as follows:

1. Triangulation is used to compared the measured attributes of signals from satellites
2. For this process, the receiver must measure the distance between itself and satellites using the travel time of the signal.
3. To measure travel time, the GPS must have very accurate timing; this is achieved with some tricks.
4. Along with distance, the exact position of satellites in space are needed. This is done by putting the satellites on a high orbit and using careful monitoring.
5. Corrections must be made for any delays the signal experience as it travels through the atmosphere.

It should be noted that location positioning is one-way; from the satellites, the information goes to the GPS device and stays there until communicated via another channel. It is important to understand that GPS systems *do not* talk to satellites, they only listen to them.

## Currently Operating Navigation Systems

There are several satellite based navigation systems currently in operation; these include GPS, Galileo, GLONASS and BeiDou.

### Global Positioning System (GPS)
This was the first navigation system to be built, and is formed from a constellation of 24 satellites and their associated ground stations. It was developed and owned by the U.S. government. There are both civilian-standardized and confidential millitary code signals coming from the satellites.


### Galileo

This is the EU's answer to GPS and is maintained by the GNSS agency, with headquarters in Prague, Czech Republic.

### GLONASS

Russian owned; also has 24 satellites and similar precision to GPS.

### BeiDou

Officially called the BeiDou Navigation Satellite System (BDS), this Chinese system is also known as COMPASS or BeiDou-2. It has been operational since December of 2011 with a partial constellation of 10 satellites - and since December of 2012, has been offering services to customers in the Asia-Pacific region.

## Triangulating Position

Mathematically speaking, four satellite ranges are needed to determine exact positioning, given perfect timing. This is not achievable with current technology, so more are needed.  

![[Pasted image 20220117163044.png]]

If the receiver's clocks were perfect, all satellite ranges would intersect at a single point (the position). To check if they are not, we require the fourth range to act as a cross-check. 

With imperfect clocks, the cross-check does *not* intersect with the first three measurements, allowing the device to detect a discrepancy, and conclude that its clocks are not synchronised with universal time. 

Since any offset will affect every measurement, the receiver looks for a single correction factor to subtract from *all* of its timing measurements, that would 'cure' the timing offset and cause all ranges to intersect at a single point. As a result, this correction brings the receiver's clock back into sync.

It should be noted that GPS gives not only the position at which we stand; it also is a source of syncing time precisely with satellite time - since satellites keep precise atomic time, by synchronising, so do our devices.

## Caveats of GPS

Signals may bounce off of local obstructions before our receiver obtains it. This is called a *multipath error* and is similar to the ghosting effect seen on TV. Good receivers use sophisticated signal rejection techniques to minimise this effect.

GPS as a whole relies on the idea that a signal can fly straight from the satellite to receiver. Unfortunately in reality, signals bounce off most things in a local environment and will get to the receiver in this manner (as well as directly). 

![[Pasted image 20220117163926.png]]

This results in a barrage of signals, first the direct transmission, then a delayed set of reflected signals; which creates a messy resultant signal. If the reflected signals are strong enough, the receiver can be confused into making erroneous measurements.

Good receivers deal with this through various signal processing tricks, to make sure that only the earliest arriving signals (the direct ones) are considered. Sometimes, additional signals from base stations are added to the positioning signal; these base stations provide the difference between actual and measured delay (for all visible satellites), thus improving accuracy. This approach to things is referred to as differential GPS (DGPS).

If a loss of signal occurs (e.g. the receiver is in a tunnel), a so-called *intertial* measurement takes place; the last location (or last fix) is combined with road knowledge and the readings for travelled distance of the device are combined for accurate measurement - a process called *dead reckoning.* Sophisticated intertial systems make use of sensors such as accelerometers, gyroscopes and magnometers to do this.



