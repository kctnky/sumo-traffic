## Highway Traffic (Bidirectional, Shorter in Length and Tİme)

This simulation is created by shortening the length in two-way highway traffic scenario in order to decrease simulation time and load. Total simulation time is also compressed such that shape of the vehicle generation plot is kept as same with the original plot but the time axis is scaled. Check [highway-synthetic](https://github.com/kctnky/sumo-traffic/tree/master/highway-synthetic) for more details about the road network, traffic demand and simulation details.

### Summary

* Total 4 kilometers in length
* Bi-directional, 2x3 lanes
* Speed limit is 130 km/h
* There are 4 different kinds of vehicles: Normal Car, Fast Car, Overland Bus, Truck
* Vehicle generation can be approximated as Poisson distribution whose mean changes with respect to hour of the day
