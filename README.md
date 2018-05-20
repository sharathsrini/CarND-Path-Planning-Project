# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
 

![alt text](https://s3-eu-west-1.amazonaws.com/elasticbeanstalk-eu-west-1-981246043789/wp-content/uploads/2018/03/16110823/car-path-planning.png)



### Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.



#  My take on the CarND-Path-Planning


![alt text](https://s3-eu-west-1.amazonaws.com/elasticbeanstalk-eu-west-1-981246043789/wp-content/uploads/2018/03/16105859/Shem.jpg)

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

![alt text](https://s3-eu-west-1.amazonaws.com/elasticbeanstalk-eu-west-1-981246043789/wp-content/uploads/2018/03/16111923/car-parking.png)

#### Condition to check:

##### Centre Lane

 * If car is not going to change  lane , maneuver to find the best action
 * Check if the car is in center lane
 * Check if the this lane is blocked
 * Check if the other lanes are also blocked
 * Check if the car is faster than the front car
 * Check if the car is not faster than the front car
 * Check if  only the left lane is free
 * Check if the right lane is free
 * Check if the both lanes are free
 * Check if the current lane is free
##### Left Lane
 * Check if the car is in left lane
 * Check if the this lane is blocked
 * Check if the the center lane is also blocked
 * Check if the ego car is faster than front car
 * Check if the ego car is not faster than front car
 * Check if the center lane is free
 * Check if the Left lane is free

##### Right Lane

 * Check if the car is in right lane
 * Check if  this lane is blocked
 * Check if the the center lane is also blocked
 * Check if the ego car is faster than front car
 * Check if the ego car is not faster than front car
 * Check if the center lane is free
 * Check if the the right lane is free


For behaviour planning the algorithm-:

1. The car estimates for safety  30 m ahead , it actually tries to find other cars in the lane.
2. If a car is sensed 30 m ahead,  provided it is moving slow , we  will try to switch the lane.
3. We will check the left lane first, if it is free and has no vehicle ahead  30 m and no vehicle  10 m behind the car. We check for the Behind proximity because while changing lanes, collision can happen with the cars that are moving point to point parallelly.
4. If the left lane is not available, as in free then it checks to switch to right lane, if it is free and has  no vehicle ahead for 30 m and 10 m behind the car.
5. If we are left with no option for changing the lane, then we will have to make it stay in the current lane without colliding with the car ahead.


### Trajectory Generation 

![alt text](https://s3-eu-west-1.amazonaws.com/elasticbeanstalk-eu-west-1-981246043789/wp-content/uploads/2018/03/16111653/block.png)

In this module, the actual trajectory of the self-driving car is determined. Therefore, the previous planned path is used as first waypoints if it consists more than two points. Otherwise, the stored reference point is used. Moreover, three farther points are added at distances of 50m, 60m and 90m. Next, these list of waypoints is transformed back in local coordinates to be used by the spline library. Again, if there is already a planned path, it is used as starting point for the trajectory. Next, 50 points are equally interpolated in a path of a distance of 30m. This includes the information of the behavior module, so acceleration and decelerations are considered in the distances of two consecutive trajetory points. And last but not least, the points are transformed back in global coordinates.


