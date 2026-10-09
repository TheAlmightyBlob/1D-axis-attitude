Single-axis 6U CubeSat-like satellite attitude control (PD Controller)

AI guidance was used for planning and debugging. Fully coded in MATLAB.

Model:
6U CubeSat-like, m = 12 kg, I = 0.12 kg.m^2 (assumed). Target angle: 0.52 rad or 30 deg. Run length of 120s.
Second-order ODE for rotational mechanics notions were used (ie. torque, angular velocity)
Two states taken in ode45 are theta and omega by newton's second law of rotational motion, in radians.

Limitations:
Single axis, no disturbances, assumed as a uniform shape.

Code:
- plots theta and omega for discrete values of theta, omega, tau
- implements P controller
- implements damping (PD Controller)
- implements rise time, overshoot (%), settling time, and steady-state error

Results:
At Kp (proportional controller gain) = 0.1 and Kd (damping gain) = 0.22, a damping ratio of approx 1.00 is found.
Results of rise time (s), overshoot (%), settling time (s) when Kp and Kd are varied, with the resulting damping ratio:

    Kp      Kd      DampingRatio    RiseTime(s)    Overshoot(%)    SettlingTime(s)    Steady-State error(rad)
    ___    _____    ____________    ___________    ____________    _______________    _______________________

    0.1    0.002     0.0091287        1.0834            97.152            NaN                 0.036995       
    0.1     0.02      0.091287         1.205            74.968         45.565               3.0293e-09       
    0.1     0.18       0.82158        2.8042            1.0807         4.3633               1.3204e-10      
    0.1     0.22        1.0042        3.7217        2.0916e-07         6.4907               6.1129e-11       
    0.1      2.2        10.042        48.193                 0         85.925               6.0274e-07       

However, we can see that at a damping ratio of 0.82 for Kd = 0.18, we get a shorter settling time of 4.36s with minimal overshoot of 1.08%, and negligible steady-state error.
This demonstrates that it can be worth sacrificing slight overshoot if it improves settling time substantially enough.

