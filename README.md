# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
 
./car-path-planning.png



### Simulator.
You can download the Term3 Simulator which contains the Path Planning Project from the [releases tab (https://github.com/udacity/self-driving-car-sim/releases/tag/T3_v1.2).

### Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

#### The map of the highway is in data/highway_map.txt
Each waypoint in the list contains  [x,y,s,dx,dy] values. x and y are the waypoint's map coordinate position, the s value is the distance along the road to get to that waypoint in meters, the dx and dy values define the unit normal vector pointing outward of the highway loop.

The highway's waypoints loop around so the frenet s value, distance along the road, goes from 0 to 6945.554.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

Here is the data provided from the Simulator to the C++ Program

#### Main car's localization Data (No Noise)

["x"] The car's x position in map coordinates

["y"] The car's y position in map coordinates

["s"] The car's s position in frenet coordinates

["d"] The car's d position in frenet coordinates

["yaw"] The car's yaw angle in the map

["speed"] The car's speed in MPH

#### Previous path data given to the Planner

//Note: Return the previous list but with processed points removed, can be a nice tool to show how far along
the path has processed since last time. 

["previous_path_x"] The previous list of x points previously given to the simulator

["previous_path_y"] The previous list of y points previously given to the simulator

#### Previous path's end s and d values 

["end_path_s"] The previous list's last point's frenet s value

["end_path_d"] The previous list's last point's frenet d value

#### Sensor Fusion Data, a list of all other car's attributes on the same side of the road. (No Noise)

["sensor_fusion"] A 2d vector of cars and then that car's [car's unique ID, car's x position in map coordinates, car's y position in map coordinates, car's x velocity in m/s, car's y velocity in m/s, car's s position in frenet coordinates, car's d position in frenet coordinates. 

## Details

1. The car uses a perfect controller and will visit every (x,y) point it recieves in the list every .02 seconds. The units for the (x,y) points are in meters and the spacing of the points determines the speed of the car. The vector going from a point to the next point in the list dictates the angle of the car. Acceleration both in the tangential and normal directions is measured along with the jerk, the rate of change of total Acceleration. The (x,y) point paths that the planner recieves should not have a total acceleration that goes over 10 m/s^2, also the jerk should not go over 50 m/s^3. (NOTE: As this is BETA, these requirements might change. Also currently jerk is over a .02 second interval, it would probably be better to average total acceleration over 1 second and measure jerk from that.

2. There will be some latency between the simulator running and the path planner returning a path, with optimized code usually its not very long maybe just 1-3 time steps. During this delay the simulator will continue using points that it was last given, because of this its a good idea to store the last points you have used so you can have a smooth transition. previous_path_x, and previous_path_y can be helpful for this transition since they show the last points given to the simulator controller with the processed points already removed. You would either return a path that extends this previous path or make sure to create a new path that has a smooth transition with this last path.

## Tips

A really helpful resource for doing this project and creating smooth trajectories was using http://kluge.in-chemnitz.de/opensource/spline/, the spline function is in a single hearder file is really easy to use.

---

## Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `install-mac.sh` or `install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!


## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

#  My take on the CarND-Path-Planning


./Shem.jpg

## Path Planning Project
The goal of this project is to drive a car around a simulated highway including traffic. In all previous projects we just used to drive only our car around the track, but this was a bit different. The simulator tries to inact the actual highway situation and we just need to write our code in such a way that car drives better than we drive!!! As always there are a number of constraints-:

* The car should not exceed the speed limit of 50mph on the highway
* Lets make sure the car does not exceed a total acceleration :  10 m/s^2
* Lets make sure the car does not exceed a total jerk : 10 m/s^3
* The car should  not have collide with any of the other cars while it changes lanes or driving inside a lane.
* The car should stay on its lane, except for the time when it  changing lanes.
* If the car ahead is too  slow, then we should be able to change lanes and overtake the other car safely.

## Rubric Points

1. *The Code compiles correctly.*- The code complied successfully. I had used the spline approach for smoothening and fitting a proper spline into the trajectory.

2. *The car is able to drive at least 4.00 miles without incident.* - The car drove around the highway easily. 

3. *The car drives according to the speed limit.*- As I mentioned in Point 2 the car drove without any incidents, and maintaining speed limit for one of the incidents. The car drives at a max speed of 49.5 if there is no slow moving traffic ahead of car, if the car encounters a slow moving traffic, it tries to change the lane. If lane change is successful, then well and good otherwise car will lower its speed and keep moving in the same lane.

4. *Max Acceleration and Jerk are not Exceeded.* - True, the acceleration and jerk were in prescribed limits. If there is slow moving traffic ahead the car's acceleration is reduced by 5mph and immediately from 49 to 18 as it will produce a lot of jerk. Same is the case with the acceleration, it accelerates smoothly by 5mph.

5. *Car does not have collisions.*- There were no collisions, there were one or two incidents where there were collisions while changing lanes, but proper code was then implemented which I will explain in the pipeline.

6. *The car stays in its lane, except for the time between changing lanes.*- The car stays inside the lane, we are just responsible for providing the lane number, the control section is handeled by the simulator.

7. *The car is able to change lanes*- Whenever there is a slow moving traffic the car tries to change the lane and it does it successfully if there are not cars nearby.

8. *There is a reflection on how to generate paths.* Described below.

## Model Documentation

The simulator sends a number of messages like the Car's location, velocity, yaw rate, speed, frenet coordinates and sensor fusion data.  I have used a  spline function, which fits a line to given points in a fairly smooth function.I decided to use spline as it is a well made library which will eventually reduce the computation. After fitting a line, we then feed points along that line back to the simulator.

### Prediction

The data from the sensor fusion and simulator is used to generate the estimate i.e. predict  what the other vehicles are likely to do. The sensor fusion data that gives us the data about the other cars nearby and we will have to predict what they are likely to do. We will change our behaviour on the basis of the Prediction of other cars behaviour

### Behaviour Planning 

./car-parking.png


For behaviour planning the algorithm-:

1. The car estimates for safety  30 m ahead , it actually tries to find other cars in the lane.
2. If a car is sensed 30 m ahead,  provided it is moving slow , we  will try to switch the lane.
3. We will check the left lane first, if it is free and has no vehicle ahead  30 m and no vehicle  10 m behind the car. We check for the Behind proximity because while changing lanes, collision can happen with the cars that are moving point to point parallelly.
4. If the left lane is not available, as in free then it checks to switch to right lane, if it is free and has  no vehicle ahead for 30 m and 10 m behind the car.
5. If we are left with no option for changing the lane, then we will have to make it stay in the current lane without colliding with the car ahead.


### Trajectory Generation 

The trajectory is calculated based on the car 's speed, the speed of  other cars, current lane, intended lane and past points. To make trajectory smoother, we add the  last two points. If there are no previous points then we calculate the estimate of the previous points from the current yaw and  car coordinates. Also the  three points are added in next 30-90 meters with a step size of 30 metres to trajecotry. All these points are transformed to car reference angle.


