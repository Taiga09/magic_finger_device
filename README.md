# Magic Finger, Interactive Device with p5.js
IXD256_final_taigaH, FA'22, 12/14/22
IMU sensor with p5.js

## Final Project Description: 
This assignment is the beginning of the Final project for this course. As with the last project, your prototype should include inputs (sensors, buttons, switches, etc.) and outputs (lights, sound, actuators like servos, motors, relays) that have a relationship between each other expressed through interaction and implemented with code/software and electronics/hardware.

In addition, the project should incorporate a cloud/IoT (Internet of Things) component that features some form of remote communication/operation.  In this context, a part of your project may exist online as a visualization, virtual object or some other expression or action that does not have to have visual form.  You can also consider 2 physical objects connected through the cloud (although this would likely require you to obtain an additional programmable microcontroller with network connectivity).

Besides the technical requirements the project is quite open-ended, so try to be imaginative with your concepts and aim for something that you can enjoy creating and experimenting with in the remaining weeks and hopefully beyond this course as well.

## Introduction:
I had 2 big initial ideas, which are using IMU(Inertial Measurement Unit) sensors or Capacitive sensors to control or create sketches on p5.js. I decided to use IMU sensor, in the end. For this concept, I was inspired by this project. [Finger User Interface](https://experiments.withgoogle.com/finger-user-interface)

## Implementation:
Explain your process of prototype development including all applicable aspects such as hardware (electronics), firmware (arduino code), software (p5.js or other code), integrations (Adafruit IO, IFTTT, Arduino IoT cloud, etc.), enclosure and mechanical design. Use a separate subheader for each part:

### Hardware(Electronics):
Things I used: M5 Stack board, M5 Extension, IMU(Inertial Measurement Unit) sensors, Strap, USB C-C cable, Tape.  
![IMU_hardware](https://user-images.githubusercontent.com/118408939/207998460-e69c7d56-b344-42b0-88ba-bc0b7a962c9d.jpg)
![IMU_sensor_bb](https://user-images.githubusercontent.com/118408939/208061272-6aee2e29-3814-433c-a484-9d3e189ed4b9.jpg)

### Firmware:
[Arduino file](https://create.arduino.cc/editor/taiga12/88f52f17-0aa0-4d80-be52-31f066dd38c8)

I'm getting Accelerometer x,y,z and gyro x,y,z from the IMU sensor to control Force Vectors in p5.js.

### Software:
[p5.js sketch](https://editor.p5js.org/tharuyama/sketches/hRd596Xwx)

The code below enables me to control different force vectors smoothly. This is where it took me a while to figure out. It was hard to set the specific value ranges. I ended up having the nested conditions and the minimum, maximum range of 2 values in the array. Also, I had no idea that the IMU sensor has defined directions, so I was confused to get the specific values.
```
// Store values into arrays
accXData[dataCounterx] = accX;  
accYData[dataCountery] = accY;

if(dataCounterx < num)
  dataCounterx += 1;
else
  dataCounterx = 0;

if(dataCountery < num)
  dataCountery += 1;
else
  dataCountery = 0;

//Push Right
if (accXData[i] > 5){
  if (0 < accXData[i] - accXData[i-1] < 2){
      for (let j = 0; j<num; j++){
        console.log('Right');
        particles[j].addForceA();
      }
  }
}
```
This is trivial, but it was actually important in terms of the visual. The code below enables us to see the paths of the particles while keeping them on the canvas. Using backgdround(255) wouldn't make this effect.
```
//Filter
push();
translate(-width/2,-height/2);
noStroke();
fill(255,80);
rect(0,0,width,height);
```
The code below creates +x directional force and adds it to the particles' velocity.
```
// +X direction
this.forceA = createVector(0.006,0,0.003);
this.alpha = this.forceA.div(this.mass);

addForceA(){
    this.acceleration.add(this.alpha);
    this.velocity.add(this.acceleration);
  }
```
### Enclosure:
![装着イメージ](https://user-images.githubusercontent.com/118408939/207998802-88e010ef-d50f-4f1b-b14f-6222d2ac0eec.jpg)

## Project outcome:
I was able to create the Finger Interaction(control my sketch with a finger), which I wanted to do. And I'm happy with the final visual.

*Find a video in a folder.*
<img width="1440" alt="Screenshot 2022-12-16 at 13 28 18" src="https://user-images.githubusercontent.com/118408939/208256616-396337e6-6f6c-476f-8cc5-2c2e43e2a19a.png">
<img width="1440" alt="Screenshot 2022-12-16 at 02 56 10" src="https://user-images.githubusercontent.com/118408939/208256623-8df72d7d-38b2-47af-af8e-c45fdc5c0426.png">


## Conclusion:
At first, I was planning to use a finger to draw a new sketch on a canvas. However, during my time with the IMU sensor, I found it very difficult to control a sketch as the IMU sensor just detects accelerometer x,y,z and gyro x,y,z, not the locations. And realized that I should have used a capacitive sensor for that concept as it detects x,y,z locations of my hand. As for next steps, I would study and use TensorFlow to detect specific gestures to control my sketch in a more interesting way.

## Project references:
https://www.youtube.com/watch?v=fBqaA7zRO58

A book - Processing, Creative Coding by Atsushi Tadokoro


