## Wilfred Githuka
## Udacity Path Planning Project Documentation

This is the documentation to gether with the requirements for passing the project.
There two versions of this documentation: This one and the simple abridged version.
Both documnentations are available in Chinese and English.

## Introduction
The path planning project is by far the most interesting project after Behavioral Clonning
Project. This project is for Term3 (Last Term) and it is the first project for this term. 

The mian objective is to create a path planner that will be able to safely and smoothly
create a path fo a vehicle to follow along on a 3 lane highway traffic.It should be able to keep
inside its lane, avoid hitting other cars and pass slow moving traffic all by using localisation,
sensor fusion and map data. When passing other cars it should not hit them.

### Technical Stats (Vehicle & Track)
* Vehicle Weight: Unknown
* Track Distance: 6,945.554m ~7km
* Legal Speed: 50mph ~ 80kph
* Acceleration: <10m/s
* Legal Jerk:

## Getting Started
The first thing I need to do is to move the car in our simulator and see the response. I will
move it in a straight line at the max legal speed of 50mph (80kph). So in main.cpp instead of setting
the speed directly, we pass next_x_vals and next_y_vals to the simulator. I then set the waypoints to be
0.5m apart (50cm). Since the car moves at 50 times/sec, a distance of 0.5m (50cm) will create a velocity of
25m/s which is close to our 50mph.

![image01](/images/Car_Move_Straight_Line.png)

The car responded and moved but just in a straight line from 0 to 56mph in a single 20ms frame which caused 
a sharp rise in acceleration. The result of this was a jerk which would be very uncomfortable for any people 
in that car. For a comfortable ride, the total acceleration should be well below 10m/s. I also had to comment
out a line of code: auto sensor_fusion=j[1]["sensor_fusion"]; for it to compile. For now I dont know what it
does really but the car moves. Great

One major issue to the problem above was that the car was veering off the road in just a straight line. 
We need to make sure that the car stays within the lane and for that we will opt for frenet cordinates which
give us the distance and deviation values which we can work with to ensure that the vehicle stays on the lane.

## Rear-Ending Other Cars
I managed to solve the driving-in-a straight line by calculating the trajectory of the vehicle instead of directly
feeding the trajectory as I had done earler. This can be seen in the image below. 

![image02](/img/Car_Move_But_Hits_Other_Vehicles.png)

But now I have developed another problem such that my vehcile is rear-ending other cars on the same lane. 
I thought I would be able to solve this by reducing the value of dist_inc down to 0.3 from 0.5. 
This woked only on a conditon that the vehicle infront of me was not slowing down. Also my car is 
violating jerk and acceleration laws.
