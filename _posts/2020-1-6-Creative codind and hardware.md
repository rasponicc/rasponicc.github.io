---
layout: single
title: "First attempt at a data driven generative system"
date: 2020-1-6
categories: hardware creative-coding
tags: p5.js generative-art
permalink: /data-driven-system/
header:
  image: /assets/bubbles.jpg
  overlay_image: /assets/bubbles.jpg 
  teaser: /assets/bubbles.jpg
---



Goal: Use real time sensor data to make art.

Ever since I came across Processing foundation and plethora of ways to make art I've wanted to try this out. Even though I'm far,far away from making Refik Anadol like artwork, I wanted to blog my first attempt at a real time data driven system. So here it goes!
<hr>

I tried to take inputs from an Arduino to control graphics in processing.  Now the initial project I thought of was of course very ambitious, but I managed to convince myself to take baby steps. I wanted to manipulate the basic random bubbles programme.

```
void setup() {
  
  size(500,500);
  background(255);
  noStroke();
  
}

void draw() {
for(float i=0; i<100; i++){
        float x = random(width);
        float y = random(height);

        fill(255,0,140,100);
        ellipse(x,y,60,60);
}
  }
```
![Random-bubbles](/assets/bubbles.jpg)

Instead of the number of circles depending on a fixes value (i<100), I wanted them to change based on some real time inputs. So I hooked up a potentiometer and using it's input's tried to  control the bubbles.

First, I had to figure out a way to make the Arduino communicate with processing. This was done using the serial library. I was able to display the potentiometer values in the console in Processing. Next based on that value I wanted the bubbles to appear and dissapear.

The code at the end looks something like this:

```
  
import processing.serial.*;

int lf = 10;    // Linefeed in ASCII
String myString;
Serial myPort;  // The serial port

void setup() {
  // List all the available serial ports
  printArray(Serial.list());
  // Open the port you are using at the rate you want:
  myPort = new Serial(this, Serial.list()[32], 9600);
  myPort.clear();
  // Throw out the first reading, in case we started reading 
  // in the middle of a string from the sender.
  myString = myPort.readStringUntil(lf);
  myString = null;
  size(500,500);
  background(255);
  noStroke();
}



void draw() {
  while (myPort.available() > 0) {
    myString = myPort.readStringUntil(lf);
    if (myString != null) {
     // println(myString);
      float f = float(myString);
      println(f); 
      
      for(float i=0; i<f; i++){
        float x = random(width);
        float y = random(height);
        float[] floatArray;
        floatArray = new float[x];

        fill(255,0,140,100);
        ellipse(x,y,60,60);
  }
    }
  }
  
}
```
At the end it ended up looking like this:<br>
!video [random bubbles](/assets/bubbles.mp4)

<video width="480" height="320" controls="controls">
  <source src="/assets/bubbles.mp4" type="video/mp4">
</video>

I can control the rate of bubbles appearing however, I want to make them dissapear as well when I reverse the knob of the potentiometer and the value goes down. Gonna try more till I a lot make this possible. Anyhow, I love this project and see a lot of scope with new ideas here!
