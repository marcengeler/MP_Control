# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

The basics for the Model Predictive Control Algorithm lie in the underlying model of the vehicle.

[balance]: ./vehmodel.PNG "Vehicle Model"
![alt text][balance]

To optimize the behavior of the control algorithm, the cost has to be defined beforehand. because the driving direction is the most important attribute of the control mechanism, it was weighted the highest:

J = 250 * dx ^ 2 + 1000 * dpsi ^ 2  + dv ^ 2  + 50 * steer ^ 2 + throttle ^ 2 + 100000 * dsteer ^ 2 + dthrottle ^ 2

where dx denotes the relative distance to the center point of the road, dpsi the deviation from the relative direction of the path, dv the remaining velocity to the desired velocity, steer the steering angle, throttle the throttle position, and dstreet and dthrottle the relative change of the throttle and streeting angle.

dsteer and dthrottle cost will decrease the change rate of the control outputs. This is important to reducde erratic control behavior and will actually smooth out noise on the input, which will then not be fed through to the control output. the dv part actually handles the cruise control, whereas dc and dpsi handle the driving direction.

Although it is important to control dx and dpsi the most, taxing the control inputs to get a better noise behavior is also important.

Another two parameters which cen be controlled are dt and N, where dt denotes the timestep between control actions and N denotes the number of extrapolation points. denoting 10 for N and 0.1 for dt worked out really well. It is possible to reduce N to get a better computational performance, however, having a greater N allows to adjust the trajectory more to the future position of the road and to look further ahead while controlling the vehicle.
