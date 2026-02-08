---
title: "XYZ Gripper Robot"
date: 2022-10-17T23:57:37-04:00
draft: false
type: page
---
Completed: April 2022
{{< youtube V6Dm7wGGrKQ >}}

This was my final year capstone project. The client for this project was a material sciences professor. For his research, his group completes many compression tests of 3D printed components, so our project revolved around removing tedious parts of his project. There were different aspects of the testing process that we could have focused on, but we decided to make a robot that automates the queueing, loading and removal of test samples.

{{< youtube -Vy11onMYCo >}}

After following the engineering design process, the final result can be seen in the video above. The XYZ Gripper robot moves between 12 positions in the queueing area, grabs a test sample and then moves it onto the test platform. The gripper has a force sensor, so it is able to detect any sample between 25 mm and 75 mm. The robot moves in the x and y directions using a belt and stepper motor, and the z direction is driven by a lead screw.

{{< figure
 src="/images/projects/gripperdrawing.png"
 alt=""
 caption="Drawing of the gripper forces"
 class="ma0 w-75"
 width=100%
>}}  

One of my tasks was designing the gripper system for the project. First, I looked at potential gripper designs that were relevant to the problem. I narrowed it down to a rack and pinion gripper due to form factor and simplicity of the mechanism. From there, I calculated the force required by the fingers to lift a sample and then found the required torque the motor would need to provide. Then a motor was selected based on its stall torque and its ability to have force detection. After the motor, I began to CAD the gripper, focusing on designing for assembly. I decided to 3D print the gripper because it allowed for easy manufacturing of custom geometries for the gears, rack and housing.

This was the largest project I've been a part of, and I think the most satisfying part was putting all the components together and seeing the robot work as a whole. There was some minor troubleshooting initially, but because of our preparation, the robot was able to mostly work right off the bat. 
