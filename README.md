single-axis satellite attitude control (PD Controller)

6U CubeSat rough dimensions, mass and inertia value taken
initial conditions assume torque and angular velocity is 0

two states taken in ode45 are theta and omega by newton's second law of rotational motion, in radians
AI guidance was used for project planning and step goals

1st step: plot theta and omega for discrete values of theta, omega, tau

Initial Predictions (15:15):
if \theta = \omega = \tau = 0, then no rotational motion will occur, and \theta will stay constant
if \omega is an arbitrary constant, \theta will be plotted as linearly increasing
while \omega is an arbitrary value and \tau = 0, a straight line graph (for angular velocity) will occur
if \omega and \tau are arbitrary values, the graph will show a straight-line for \omega and a parabola for \theta
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

ratio < 0 means energy is being supplied instead of removed

ratio = 0 means there is no damping

0 < ratio < 1 means there is underdamping, with higher values meaning stronger damping, and so the target angle is reached faster.
lower values oscillate more and take longer to reach the target angle

ratio = 1 leads to the system reaching the target angle with the best balance between oscillation and time (shortest time for 0 oscillation)

ratio > 1 overdamped and system oscillates for a long time

Observations:
Predictions are generally correct, with the exception of when the ratio > 1
The system does not oscillate in this case and instead very slowly progresses towards the target angle.
This is likely due to a damping ratio > 1 causing the system to brake too strongly, leading to a very slow movement.

Additionally, when ratio = 1, it is not only the best balance between oscillation and time, but there is no oscillation whatsoever, 
on top of the target angle being reached very quickly
results for a ratio = 1 were theta = 0.52 rad being reached in approx 5 seconds.

next step: Implementing rise time, overshoot (%), settling time, and steady-state error

Assumptions:
Rise time is taken from 10% to 90% of the target angle since it is assumed that values outside of this range are more prone to noise

Predictions:
overshoot, rise time, and settling time will vary when damping ratio is varied.
damping ratio closer to 1 means a smaller overshoot and lower rise & settling time
damping ratio < 1 means a larger overshoot and longer rise & settling time
damping ratio > 1 means a smaller overshoot and longer rise & settling time

Steady-state error represents the difference between the final achieved angle and the target angle.

Observations:
All predictions were correct, except that rise time decreases with damping ratio, 
since less damping means there is less braking on the PD controller, by consequence reaching 90% of the target angle sooner.
Something to take note of is that as rise time decreases for damping ratio < 1, the settle time and overshoot increases. 
This shows that even though the rise time is better, the overall model is optimal at values nearer to 1.

Results:
At Kp (proportional controller gain) = 0.1 and Kd (damping gain) = 0.22, a damping ratio of 1.00 is found
Results of rise time (s), overshoot (%), settling time (s) when Kp and Kd are varied, with the resulting damping ratio:

    Kp      Kd      DampingRatio    RiseTime(s)    Overshoot(%)    SettlingTime(s)    Steady-State error(rad)
    ___    _____    ____________    ___________    ____________    _______________    _______________________

    0.1    0.002     0.0091287        1.0834            97.152            NaN                 0.036995       
    0.1     0.02      0.091287         1.205            74.968         45.565               3.0293e-09       
    0.1     0.18       0.82158        2.8042            1.0807         4.3633               1.3204e-10      
    0.1     0.22        1.0042        3.7217        2.0916e-07         6.4907               6.1129e-11       
    0.1      2.2        10.042        48.193                 0         85.925               6.0274e-07       

However, we can see that at a damping ratio of 0.82 for Kd = 0.18, we get a shorter settling time of 4.36s with minimal overshoot of 1.08%, and negligible steady-state error.
This demonstrates that it can sometimes be worth to sacrifice slight overshoot if it improves settling time substantially enough.