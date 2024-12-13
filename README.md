# ME 405 Final Project: Romi Time Trials and Final Deliverables 
## Features of the Romi
<div align="center">
  <img src="https://github.com/user-attachments/assets/eee2ba06-a4db-4f68-a96d-1ed20a6bf5d9" alt="image" width="300">
</div>

For this project, we were provided the Romi chassis, motor driver, power distribution board, and a romi encoder pair kit. The goal for this project was to get Romi to follow the maze, which includes squiggly lines, straight lines, and an obstacle. The Romi is not able to move holonomically, but it can spin in place and allow turns. In addition to the Romi-specific components that were listed earlier, we have an IMU (Inertial Measurement Unit) called the BNO55. The IMU provides sensor data to Romi so that Romi's navigation skills are enhanced. This information supplements the wheel encoder data, as the encoder data gives real time movement data while the IMU gives orientation/position information that betters Romi's performance. 
<div style="text-align: center;">
  <a href="https://www.pololu.com/product/4022">Romi Kit Link</a>
 </div>


## Sensors 
We planned to use 1 bumper sensor and 3 line sensors. The bumper sensor would detect collisions or impacts with objects, which was useful as the final maze includes an obstacle. The line sensors were the star of the show, as the Romi is programmed to follow the black line on the maze. It works by adjusting its motors based on inputs from the line sensor. If the sensor detects the line on the left, it should turn left to realign, and vice versa. Together, these sensors would enhance the robot's ability to naviage autonomously. 
<div align="center">
  <img src="https://github.com/user-attachments/assets/afb83e88-ba85-4fed-a0c5-61c4ca6973fd" alt="image" width="300">
  <img src="https://github.com/user-attachments/assets/ccf53c6c-6019-484d-a365-e019ce8df435" alt="image" width="200">
</div>

<div style="text-align: center;">
  <a href="https://www.robotshop.com/products/infrared-line-tracking-sensor">Line Sensor Link</a>
 </div>
 
<div style="text-align: center;">
 <a href="https://www.robotshop.com/products/bumper-sensor-robot">Bumper Sensor Link</a>
</div>

### Sensor Brackets 
We were planning to use 1 middle bracket and 2 side brackets, shown here on the Romi.

The goal of the brackets were to attach them securely to the Romi. The original plan was to use one side bracket design, but due to the middle part of Romi not being flat like the sides, we created an additional middle bracket design. The following links below are stl files for the brackets. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/f26290a6-3893-4a67-b77a-b78455e28032" alt="image" width="400">
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/faa896ba-703a-4afe-8dc4-3c55742d33d9" alt="image" width="400">
</div>

[Download the Middle Bracket STL file](https://github.com/skim314/ME405.github.io/blob/main/middlebracket_print_2.STL)

<div align="center">
  <img src="https://github.com/user-attachments/assets/ca9770cc-f1b8-4c44-8d1f-ba43e0fb8923" alt="image" width="400">
</div>

[Download the Side Bracket STL file](https://github.com/skim314/ME405.github.io/blob/main/sidebrackets_print_4.STL)

## Code Explained
There are 8 seperate py files in the zip file: bump sensor, cotask, encoder, i2c, line sensor, motor, task share, and main. 

### Bumpsensor.py
In this code, we are defining a python class, "BumpSensor". This is designed to detect when the bump sensor is triggered. The is_bumped detects a change when the sensor is pressed, as then the pin state would change from high to low. The wait_for_bump monitors the sensor state and halts execution until there is a bump detected.

### cotask.py
This file defines a multitasking framework to manage cooperative task execution. It is a generator-based approach where the tasks yield control to the scheduler. This allows time-sharing between tasks. This is ideal for embedded systems where resources are limited, and it is useful as it allows control over task execution timing and prioritization. 

### encoder.py
We are defining an encoder interface for measuring position as well as speed. This is beneficial for our application as Romi requires precise position and speed measurement for following the maze path. 

### i2c.py
We are defining a python class (BN055) for interfacing the IMU. This provides methods to retrieve calibration data, read angular velocity, orienation, and for configuring the sensor. It utilizes I2C communication to interact with the IMU. 

### linesensor.py
We are defining a module for interfacing our line sensor. It allows for detection of black or white surface colors, which is needed for the maze. It implements two classes, LineTrackingSensor and LineTrackingSensorArray. It uses ADC module to read the sensor voltages and determine the color.

### motor.py 
Our MotorDriver class enables precise direction and for speed adjustments. Here, we can control the motor by enabling/disabling, setting direction, and for adjusting effort. We use PWM (pulse-width modulation) to control motor speed using digital pins. 

### taskshare.py
This module is a framework for sharing data between tasks for a multitasking environment. It ensures that the data is not corrupted when tasks are interrupted. 

### main.py 
This is where the magic lies. This code sets up the multi-tasking system to control the robot. The system includes reading sensor data, controlling the motor, as well as closed-loop feedback control for line following. It seperates different functionalities like sensor reading, communication, etc into tasks. This allows for better maintenance of the code structure. There are also shared variables in our code, such as "right_motor_speed_share", which allows different tasks to commmunicate and exchange data. This ensures that each task is updated consistently which most recent readings from the sensor and control. Below is a snippet of our code as this shows the multi-tasking system set up.
![image](https://github.com/user-attachments/assets/6743baa3-4005-43d9-b919-ccb69d2e8c2c)


wiring diagram: 
5 for line sensor, 1 for bump sensor 




Here is the link to the zip file that includes all the required code files to run the Romi.
[Link to Zip File (https://github.com/user-attachments/files/18130081/Final.Project.zip)


## Results (Video Link)
As you can see in our video, when we put the Romi at the start line, it follows the line but then turns thinking it is following the edge of the line instead of the path. The second clip shows when we tested the squiggly path, and you can see that our Romi follows the path here. The videos were taken at the same test run, but we wanted to show that it does indeed follow the path. We will talk about future improvements in the next section. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/93e745b1-80b1-4f4c-909c-ed08b599179c" alt="image" width="400">
</div>


## Recommendations for Improvement 
#### Sensor Troubleshooting
However, we had an unexpected delay as our 2nd rendition of our 3D prints were not able to be printed in time. We attached a line sensor to an already printed out bumper sensor bracket. We ran into issues with the line sensor not following the line from the maze, so we had to start from the beginning - testing that the line sensors were correctly working on the Romi. We covered a couple of the infrared detectors on the sensor, as there are five detectors on one sensor. Our thought process was that if Romi is not correctly following the path, is there a potential issue with our line sensor?

<div align="center">
  <img src="https://github.com/user-attachments/assets/b010680d-bb3d-418d-89c5-ebd9772a6176" alt="image" width="700">
</div>

However, this was not the case as puTTY was showing the changes real time when we would cover some of the detectors and uncover them. On the picture below, we can see that our line sensor is a bit far from the ground, which is why we believe there is an influence on our Romi having trouble following the maze line. If we had time to get the new rendition of the 3d printed side brackets, the line sensor would be closer to the ground, which could help detection of the line. We also believe adding 1-2 more line sensors would have been helpful, but we wanted to focus one using one line sensor with the timeframe we had. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/f43f8dc3-7cb1-40c9-9517-1782e0f94e57" alt="image" width="500">
</div>

Then our next step was to look at our control system. 
**Talk about distance of line sensor to ground , implementing more sensors 
### Control System Troubleshooting
As you can see on our video, our Romi did not perform like we wanted it to. We were having trouble with the Romi following the main black line, it seemed to register the outer side of the paper during our trial runs. We would work on the control system, as it seems that our error resonates there. 

To give a bit of background, our control system was PID (Proportional-Integral-Derivative) control. This was because the derivative control would be useful for our case, as the derivative term acts like a damping factor by reacting to changes. This helps prevent overshooting, would means the Romi could reach the desired state (aligning to the line path) faster than P or PI control. 

We estimate that our control system has improper PID tuning, or that our logic has an incorrect implementation. If our P is too low, the robot would react too slowly, which we don't believe was the case. If our P is too high, the Romi may overcorrect and lose the line path. If our I or D is too high, the errors would stack and lead to overcorrections. To fix this, we would have to troubleshoot by adjusting the PID gains. Due to these issues, we need to review that the error is calculated correctly and that the PID terms are updating consistently. 




Emphasis, aka italics, with *asterisks* or _underscores_.

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.





Colons can be used to align columns.

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |



Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

