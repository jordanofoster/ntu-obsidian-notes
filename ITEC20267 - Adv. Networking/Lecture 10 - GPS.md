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
2. For this process, the receiver must measure the distance between itself and satellites using the travel time 