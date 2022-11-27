# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
   
### Simulator.
You can download the Term3 Simulator which contains the Path Planning Project from the [releases tab (https://github.com/udacity/self-driving-car-sim/releases/tag/T3_v1.2).  

To run the simulator on Mac/Linux, first make the binary file executable with the following command:
```shell
sudo chmod u+x {simulator_file_name}
```

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

## Rubric

### Code compiles correctly

Inside the build folder the make works perfectly and the code is compiled.

(img code compiled )

### The car is able to drive at least 4.32 miles without incident. 

#### Meaning that the car drives according to the speed limit:

Stays always slower than 50 mph.


#### Does not exceed Max Acceleration and Jerk:

No red flag during all the time, running for 15 miles.


#### Does not collide with any other vehicle at any time:

It is able to drive and interact with the traffic without any collision.


#### Stays in it's lane and it is able to change lanes:

Capable of maintain the lane when there are no traffic and to change lanes when there is a slower car ahead.


(img car track best run without incident)


### Reflection

This was a very challenging project, maybe because of the expertise needed to write better a C++ code and the lack of a software development backgrond, but a very interesting one, after hours of research and checking the mentors help by the way (thanks a lot!), and to see your code running and spend minutes watching your car drive autonomously !!

It was a huge help the Q&A lecture inside the project, way easier to understand what was going on and to have a help code to avoid a really cold start. My code ended up as a mixture of the Q&A and the mentors help, and I was able to understand it all and try other parameters to understand the consequences. So as we learned the code was divided in *Prediction*, *Behave* and *Plan the Trajectory*.

#### Prediction

Here we get the information from the sensor fusion, giving us the parameters of the other cars in range. From here we can check their d position, s position, and speed. Here we will understand if there is a car ahead of us and slower/faster, at our sides and within the 30m range, which give us the hint that it is not safe to change lanes and so decrease speed to avoid collision with the slower car ahead. One example of situation is the car ahead is slower than us, we are getting closer, and we are in the most left lane with no one at our right side, so it is safe to move right (increase lane).

Here I believe that the decrease in speed could be better tuned, as it decreases too much in order to avoid collision and the take a certain amount of time to recover, also to avoid acceleration incident. Maybe with the next class PID controller.


#### Behavior

Now we have the information regarding the traffic lets make some decisions. Here we check if there is a car ahead, and if so, we check traffic, is is safe to change lane ? 

Yes, no car at our side, lets go to our adjacent permitted lane. 
No, slow down to avoid collision.

And also if we are slower than the max speed limit, increase speed based on a diff, to avoid incident.


#### Planning

Well, last part, we check the traffic on prediction, then with this information we decided what to do, on Behavior. Now lets act !

This part calculates our path, our trajectory, based on the lane we want to go, our current coordinates and past positions. We create a vector to store those points and first we use points from our previous trajectory. After we set up some points in the future, like 30, 60 and 90 m ahead, we need to change these points to X and Y coordinates so we have pass these info to our spline function. The spline will give us back the points that connects them all in a smooth way to follow and avoid jerks.

With all the points, from previous path and the future position, the spline will give us more points based on the spline generated, so we create 50 points based on that and switch them back to the coordinates which the simulator works on, which is fed in the json msg next_x and next_y.





