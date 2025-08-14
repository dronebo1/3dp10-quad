# 3dp10-quad

A 10" 3D Printed drone made with a frame I designed myself, with the hardware:

Speedybee F405 Mini

A2212 1000Kv motors

30A 6S Readytosky ESCS

Frame design: https://cad.onshape.com/documents/6fab9e51ffb25363fd8d55d2/w/f28ccfb9a02aea8e76aa0ca1/e/93488d9bb487b8d2a32ae4b1


Update: Began PID tuning, with the goal of tuning out oscillations. 

First, I tried increasing the D term in order to increasing the damping, but increasing D term from 1 to 1.3 had no notible difference. Looking at the blackbox data, it shows that the gyro nosie is very noisy, leading to an excessively noisy D term output, which rendered the D term useless. To counter this, the gyro master filter was set to 1.3 instead of 1 in betaflight, and I also considered increasing the gyro D term filter, but changing it from 1 to 1.3 made no notible difference in the blackbox data. This led to slightly cleaner results, with far cleaner filtered gyro data, but the drone in itself still had oscillations.

Later, I tried a new approach of reseting the D term back to 1, and increasing the PI "tracking" term to 1.3, while leaving the gyro master filter at 1.3, but in hindsight, this was a mistake, as the low refresh rate of the PWM led to the drone unable to lose altitude, forcing me to disarm and leading to a crash.

I am now working on reprinting the frame in order to continue testing, as well as adding an O4 PRO mount in the canopy for some nice first person 4K footage. Once I finish reprinting and reassembling, I will try the settings:

Gyro master filter: 1.3
PI "tracking": 0.75
D "dampening": 1.3

So: to anyone trying to recreate this project: Avoid increasing PI tracking term first, and rather increase D term, and use a DSHOT digital ESC if you can, as PWM leads to more lag in the response.
