## Highway Traffic Scenario

### Road network

Road network is composed of a single double-way road having 3 lanes in each direction. Total length is about 4.25 kilometers and speed limit is 130 km/h. Each lane is by default 3.2 meters in width.

### Traffic demand

Different traffic demand options exist in which vehicle densities and total simulation time might change in each configuration. They are being followed. Select the corresponding file to simulate the desired traffic scenario. 

* **highway-24h.sumocfg**: Continuous traffic demand for a single day such that vehicle densities differ in each hour of the day.
* **highway-mu0.1.rou.xml**: Vehicle generation rate is constant and equal to 0.1 vehicles/sec throughout the simulation.
* ...
* **highway-mu1.5.rou.xml**: Vehicle generation rate is constant and equal to 1.5 vehicles/sec throughout the simulation.

It should be also noted that vehicles are summoned at the first road segment in its direction and start moving with respect to the types defined for them. A vehicle leaves the simulation when it reaches at the last road segment. 

#### Vehicle types

There are defined 4 different vehicle types:

1. Normal car:
  * Compose %40 of the all vehicles summoned during simulation
  * 5 meters in length and colored yellow in gui
  * Maximum speed is 200 km/h, Maximum acceleration rate is 2.6 m/sec, Maximum deceleration rate is 4.5 m/sec
  * Attempts to drive in random speeds of normal distribution having 117 km/h mean speed and 26 km/h deviation
2. Fast car:
  * Compose %40 of the all vehicles summoned during simulation
  * 5 meters in length and colored red in gui
  * Maximum speed is 240 km/h, Maximum acceleration rate is 3.5 m/sec, Maximum deceleration rate is 5.0 m/sec
  * Attempts to drive in random speeds of normal distribution having 143 km/h mean speed and 19.5 km/h deviation
3. Overland bus:
  * Compose %10 of the all vehicles summoned during simulation
  * 12 meters in length and colored blue in gui
  * Maximum speed is 144 km/h, Maximum acceleration rate is 1.5 m/sec, Maximum deceleration rate is 1.2 m/sec
  * Attempts to drive in random speeds of normal distribution having 91 km/h mean speed and 13 km/h deviation
4. Truck:
  * Compose %10 of the all summoned vehicles during simulation
  * 10 meters in length and colored green in gui
  * Maximum speed is 108 km/h, Maximum acceleration rate is 1.0 m/sec, Maximum deceleration rate is 0.9 m/sec
  * Attempts to drive in random speeds of normal distribution having 78 km/h mean speed and 13 km/h deviation

#### Vehicle generation

Vehicles are summoned at the first road segment with respect to the flow information defined for each vehicle type. Flow data includes a parameter which defines the probability of summoning a new vehicle to the simulation environment in each second. That results in a binomially distributed flow. It can be approximated as a **Poisson distribution** for small probabilities. 

#### Car following model

Vehicle mobility in simulation is provided by collision-free car following model of SUMO. It is a slightly modified version of the model defined by Stefan Krauss in [Microscopic Modeling of Traffic Flow: Investigation of Collision Free Vehicle Dynamics](https://sumo.dlr.de/pdf/KraussDiss.pdf). Vehicles drive in safe velocities to maintain perfect safety, i.e., they are able to avoid collisions if the leader starts braking. 

#### Lane changing model

Vehicles change lanes instantly by default in SUMO. However, different lane-changing models are also adapted for sublane simulations. In this scenario, [SL2015](https://sumo.dlr.de/docs/Simulation/SublaneModel.html) lane-changing model is configured with the lateral resolution of 0.8 meters. Considering that a sigle lane is 3.2m in width, this creates 4 sublanes.  

### Simulation

In order to start a bare SUMO simulation in the command line, type in the root folder;

> sumo -c <scenario-configuration-file.sumocfg>

### Last Words

See [SUMO Documentation](https://sumo.dlr.de/docs/SUMO_User_Documentation.html) for more. 
