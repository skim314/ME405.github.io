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


#### Sensor Troubleshooting
However, we had an unexpected delay as our 2nd rendition of our 3D prints were not able to be printed in time. We attached a line sensor to an already printed out bumper sensor bracket. We ran into issues with the line sensor not following the line from the maze, so we had to start from the beginning - testing that the line sensors were correctly working on the Romi. We covered a couple of the infrared detectors on the sensor, as there are five detectors on one sensor. Our thought process was that if Romi is not correctly following the path, is there a potential issue with our line sensor? However, this was not the case as puTTY was showing the changes real time when we would cover some of the detectors and uncover them. 

We were planning to use 1 middle bracket and 2 side brackets, shown here on the Romi. 
[Download the Middle Bracket STL file](https://github.com/skim314/ME405.github.io/blob/main/middlebracket_print_2.STL)


[Download the Side Bracket STL file](https://github.com/skim314/ME405.github.io/blob/main/sidebrackets_print_4.STL)
## Code Explained

## Results (Video Link)
[Watch this video on YouTube](https://www.youtube.com/watch?v=VIDEO_ID)




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

