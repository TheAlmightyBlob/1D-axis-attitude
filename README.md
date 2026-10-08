6U CubeSat rough dimensions, mass and inertia value taken
initial conditions assume torque and angular velocity is 0

two states taken in ode are theta and omega by newton's second law of rotational motion

1st step: plot theta and omega for discrete values of theta, omega, tau

Initial Predictions (15:15):
if \theta = \omega = \tau = 0, then no rotational motion will occur, and \theta will stay constant
if \omega is an arbitrary constant, \theta will be plotted as linearly increasing
while \omega is an arbitrary value and \tau = 0, a straight line graph (for angular velocity) will occur
if \omega and \tau are arbitrary values, the graph will be show a linear increase in \omega and a straight-line for \theta
    \theta will increase over time

Predictions have proven correct. 15:28

Next step: implement P controller

Predictions for a friction-less system(Using questions from AI):
A friction-less system will cause a P controller with too much gain to continuously oscillate around the target angle
As the target angle is reached, \tau goes towards 0 while \omega increases at a decreasing rate
If \omega > 0 when the target angle is reached, it will overshoot, and the P controller will counteract this by making \tau negative. 
Without friction, unless gain is perfect, this will continue endlessly.
The plot of \theta will look like a sine wave, if theta0 = 0
If inertia is doubled, \tau will also require to be doubled for the same rate of change of angular velocity.
Bigger Kp will mean a faster oscillation

Observations (16:17):
When the target angle is 0, theta and omega are straight line graphs, as the satellite does not need to rotate to reach the target angle.
Otherwise, regardless of target angle, omega and theta oscillate in the same manner but with different amplitudes, 
as a frictionless system repeats forever.

Next step: implement damping (PD Controller)

Predictions:
Angular velocity and theta will level off after a set amount of time, depending on the damping ratio. 
A larger damping ratio would have a greater effect and cause angular velocity to level off sooner.

ratio < 0 energy is being supplied instead of removed

ratio = 0 there is no damping

0 < ratio < 1 is underdamped, with higher values meaning stronger damping, and so the target angle is reached faster.
lower values oscillate more and take longer to reach the target angle

ratio = 1 leads to the system reaching the target angle with the best balance between oscillation and time (lowest oscillation for shortest time)

ratio > 1 overdamped and system oscillates for a long time

Observations:
Predictions are generally correct, with the exception of when the ratio > 1
The system does not oscillate in this case and instead very slowly progresses towards the target angle.
This is likely due to a damping ratio > 1 causing the system to brake too strongly, leading to a very slow movement.

Additionally, when ratio = 1, it is not only the best balance between oscillation and time, but there is no oscillation whatsoever, 
on top of the target angle being reached very quickly
results for a ratio = 1 were theta = 0.52 rad being reached in approx 5 seconds.