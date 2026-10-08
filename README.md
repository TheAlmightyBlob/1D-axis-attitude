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

Observations 16:17:
When the target angle is 0, theta and omega are straight line graphs, as the satellite does not need to rotate to reach the target angle.
Otherwise, regardless of target angle, omega and theta oscillate in the same manner but with different amplitudes, 
as a frictionless system repeats forever.