# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
   
## Modeling
The Modeling consists of multiple parts. 

### Vehicle Detection & Response
The code checks if there is a car in our current lane 30 m ahead of us. Additionally we also check if there is a car present in our left or right lane for 30 m ahead of the vehicle and 30 m behidn the vehicle. Depending on the result we set the flags too_close, left_lane and right_lane to true or false. Depending on where a different vehicle has been detected, our target vehicle decides if we wish to slow down, perform a left lane or right lane. We perform a lane change only if no vehicle is detected on the intended lane channge.

### Vehicle Trajectory

This part is described in detail in the Q & A section. Essentially we initialize a referrence velocity. We then create a list of waypoints that we will interpolate later using a spline and fill with more points to achieve the reference velocity. The reference x,y, and yaw values are determined from starting points or previous path points. If previous size is empty, we use the target vehicle's starting as reference and create tangents to the vehicle using the points, this is saved as the previous car points. These points are saved in the waypoints list. Additionally evenly spaced points are created in Frenet and are appended to the list.

To make the calculation easier for creating the spline, the coordinates are calculated to local car coordinates. Then we determine how to break up the spline so we reach the reference velocity and the rest of the path planner are filled with those points after evaluating the spline and the coordinates are transformed back to map coordinates, so we always have 50 points in the path planner and the vehicle trajectory.