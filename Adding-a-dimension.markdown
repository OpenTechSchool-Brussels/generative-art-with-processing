---
layout: default
title:  "Adding a dimension"
num: 4
---

BEWARE, Still work in progress

##a) 2 + 1 = 3D
P3D in size

primitive for drawing (box ...)

with or without background

##b) Moving in 3D (without falling...)
translate

(rotate?)

push/pop Matrix

##c) Using libraries

peasycam

```java	
import peasy.*;

PVector[] p, s, a; //The particles position, speed and acceleration
int k; // The number of particles

PeasyCam cam;


void setup() {
  size(displayWidth, displayHeight, P3D);
  cam = new PeasyCam(this, 2000);
  cam.setMinimumDistance(5);
  cam.setMaximumDistance(5000);
  
  background(0);
  noCursor();
  k = 100;
  
  // Particle array size is the number of particles we want
  p = new PVector[k];
  s = new PVector[k];
  a = new PVector[k];

  // Initialise the accelerations, speeds and positions.
  for(int i=0; i<k; i++) {
    p[i] = new PVector(0,0,0); // Center screen
    s[i] = new PVector(0,0,0);
    a[i] = new PVector(0,0,0);
  }
}

void draw() {
  //background(0);
  //Update acceleration, speed and position   
  for(int i=0; i<k; i++) { 
    a[i].set(0,0,0);
    a[i].add( new PVector( random(-1,1), random(-1,1), random(-1,1) ) );
    a[i].add( new PVector( (0 - p[i].x)/10000, (0 - p[i].y)/10000 , (0 - p[i].z)/10000 ) ) ;
    s[i].add(a[i]);
    p[i].add(s[i]);
  }

  // Draw the particles
  stroke(0);
  for(int i=0; i<k; i++) {
     pushMatrix(); 
       translate(p[i].x, p[i].y, p[i].z); // Here we use the point visual primitive
       box(30);
     popMatrix();  
}
}
```

