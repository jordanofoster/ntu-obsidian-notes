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

Mathematically speaking, four satellite ranges are needed to determine exact positioning, given perfect timing. This is not currently achievable 

