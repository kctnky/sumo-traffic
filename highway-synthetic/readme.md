## Highway Traffic (Unidirectional)

### Road network

Road network is composed of a single double-way road having 3 lanes in each direction. Total length is about 36.1 kilometers and speed limit is 130 km/h. Reverse directions are seperated from each other with a green area like in a typical highway. Each lane is by default 3.2 meters in width for conducting sublane simulations. Check *highway-synthetic.net.xml* in netedit for visualization of the road network.

### Traffic demand

Traffic demand for this scenario includes only one-way traffic, i.e. reverse direction has no traffic at all. Total traffic demand is composed for a single day such that vehicle generation rates differ in different times of the day. Vehicles are summoned at the first road segment and start moving with respect to the types defined for them. A vehicle leaves the simulation when it reaches at the last road segment. 

#### Vehicle types

There are defined 4 different vehicle types:
1. Normal car:
  * Compose %40 of the all vehicles summoned during simulation
  * 5 meters in length and colored yellow in gui
  * Maximum speed is 200 km/h, Maximum acceleration rate is 2.6 m/sec, Maximum deceleration rate is 4.5 m/sec
  * Attempts to drive in random speeds of normal distribution having 117 km/h mean speed and 26 km/h deviation
  * Can approach to the front vehicle at most 2.5 meters (see car following model below)
  * Driver imperfection is 0.4 (see car following model below)
2. Fast car:
  * Compose %30 of the all vehicles summoned during simulation
  * 5 meters in length and colored red in gui
  * Maximum speed is 240 km/h, Maximum acceleration rate is 3.5 m/sec, Maximum deceleration rate is 6.0 m/sec
  * Attempts to drive in random speeds of normal distribution having 143 km/h mean speed and 13 km/h deviation
  * Can approach to the front vehicle at most 2.5 meters (see car following model below)
  * Driver imperfection is 0.2 (see car following model below)
3. Overland bus:
  * Compose %10 of the all vehicles summoned during simulation
  * 12 meters in length and colored blue in gui
  * Maximum speed is 144 km/h, Maximum acceleration rate is 2.0 m/sec, Maximum deceleration rate is 3.5 m/sec
  * Attempts to drive in random speeds of normal distribution having 104 km/h mean speed and 13 km/h deviation
  * Can approach to the front vehicle at most 5.0 meters (see car following model below)
  * Driver imperfection is 0.1 (see car following model below)
4. Truck:
  * Compose %20 of the all summoned vehicles during simulation
  * 10 meters in length and colored green in gui
  * Maximum speed is 108 km/h, Maximum acceleration rate is 1.7 m/sec, Maximum deceleration rate is 3.0 m/sec
  * Attempts to drive in random speeds of normal distribution having 91 km/h mean speed and 13 km/h deviation
  * Can approach to the front vehicle at most 5.0 meters (see car following model below)
  * Driver imperfection is 0.1 (see car following model below)

#### Vehicle generation

Vehicles are summoned at the first segment of the highway with respect to the flow information defined for each type per hour in *highway-synthetic.rou.xml*. Flow data includes a parameter which defines the probability of summoning a new vehicle to the simulation environment in each second. That results in a **binomially distributed** flow. It can be approximated as a **Poisson distribution** for small probabilities. 

Total traffic demand for this scenario includes 24-hour flow data for vehicles. Vehicle generation rate has two peaks at 8.00-9.00 AM and 6.00-7.00 PM. It has also a local maxima at 1.00-2.00 PM. The maximum vehicle generation rate is 1.5 vehicle/sec throughout the day. As mentioned above, this probability is divided into 4 different vehicle types with respect to desired proportions of total volume. Check the reference figures given in *ref* folder. 

#### Car following model

Vehicle mobility in simulation is provided by the default collision-free car following model of SUMO. It is a slightly modified version of the model defined by Stefan Krauss in [Microscopic Modeling of Traffic Flow: Investigation of Collision Free Vehicle Dynamics](https://sumo.dlr.de/pdf/KraussDiss.pdf). Vehicles drive in safe velocities to maintain perfect safety, i.e., they are able to avoid a collision if the leader starts braking. 

#### Lane changing model

Vehicles change lanes instantly by default in SUMO. However, different lange-changing models are also supported for sublane simulations. In this scenario, [SL2015](https://sumo.dlr.de/docs/Simulation/SublaneModel.html) lane-changing model is configured with the lateral resolution of 0.8. Considering the the default lane-width of SUMO is 3.2m, this resolution creates 4 sublanes per lane. Other parameters such as maximum lateral speed for lane changing are kept in their default values of the model. 

It should be also noted that a vehicle can be located anywhere on the lane(s) when controlling the vehicle via TraCI using the command *moveToXY* for adopting and testing custom lane change algorithms in the application level. 

### Simulation

In order to start a bare SUMO simulation in command line, type in the scenario folder;

> sumo -c highway-synthetic.sumocfg

If SUMO is desired to simulate the road network via TraCI for other simulation environments such as Veins and Artery, check the corresponding documents of these tools. Normally, these tools automatically start the simulation without any action. 

The simulation settings and desired outputs to be captured are configured in *highway-synthetic.sumocfg*. By default, simulation will last 24-hour. The step length for SUMO is adjusted to 0.1 second such that SUMO will process the discretized events in every 100 ms. The instantaneous kinematic and dynamic data of randomly selected vehicles (0.01 percent of all summoned vehicles) will be stored in *out/floating-car-data.out.xml*. Total number of the passing vehicles are also counted via simulated induction loops and results will be written to *out/induction-loop-data.<LANE_ID>.out.xml* files. Then, you can use *<sumo_installation_folder>/tools/xml/xml2csv.py* to convert output files into csv format. 

### Last Words

See [SUMO Documentation](https://sumo.dlr.de/docs/SUMO_User_Documentation.html) for more. 
