---
layout: default
title:  "Adding a dimension"
num: 4
---

BEWARE, Still work in progress, especially spelling...

Well, the workshop was meant to stop at previous section, but in bonus, here is a preview of what you can do in 3D.

##a) 2 + 1 = 3D
So, first of all 3D is different than 2D. Who would have guesse. Previously, our canvas was our screen, with two axis horizontal (x) and vertical (y). Now we are adding another dimension, depth (z). But ... how can you represent a 3D world on a 2D screen? Short answer: you can't. And yet you do. We don't represent the 3D dimensions, but a 3D world, projected on the screen. Like a picture seen from a camera of a 3D world. This means that what you see on the screen depends on from where you are looking at your 3D world (the position of your camera in the 3D world). We'll get back to it later.


In our case, adding the third dimension means that we have to precise that we want to render our graphical world in 3D. For that, we just have to add one little parametre to the `size` function we used previously:

```java	
  size(displayWidth, displayHeight, P3D);
```

Previously, our center was `(width/2, height/2)` now it is `(width/2, height/2, 0)`. Z is always centered on 0, with positive value going closer to you (hence would appear bigger on screen). Try to draw a few rectangles with different depth, you'll understand better how it work.

But then again, if we're in 3D, it's to use 3D objects, not the previous 2D we used. Processing has 2 main 3D graphic primitives, `sphere` and `box`. The sphere function takes one parametere, its radius, such as in `sphere(100)`. The cube functions takes either 3 or 1 parametre. `box(10,20,30)` will define a box 10 long, 20 large and 30 deep. If you want a cube you can either call it `box(10,10,10)` or use the shortcut using only one parameter: `box(10)`. Here is one way to display a sphere:


```java	

void setup() {
  size(displayWidth, displayHeight, P3D);
  
  fill(200); // Same as for rectangle, the color of the faces
  stroke(0); // Same as for rectangle, the color of the edges
  
}

void draw() {
  background(40);
  sphere(100);
}

```



Hmmm... It is a sphere, but only part of it. This is because it is drawn in the center (0,0,0). While previous object defined implicitely there position, 3D objects don't. They need to be moved (translated or rotated). We'll see how to do that in next sessions. If we can't move the world (the sphere) yet, we can at least move our perseption of it (the camera). For that, we need a function fittingly called `camera` which (beware) takes 9 paremeters as input! Don't panic, they are actually quite simple. If you want to define a camera in 3D (imagine a real one next to you), you need to know its position (xEye, yEye, yEye: 3 parameteres), where it's looking at (xLook, yLook, zLook: 3 parameters) and last its orientation: where is "up" for the camera (xUp, yUp, zUp: 3 parameteres). So all in all:

```java
  camera( xEye,  yEye,  zEye,
          xLook, yLook, zLook,
          xUp,   yUp,   zUp);
```

Let's start with a classic, so you'll have a stable start to explore from:

```java
  // You can put all parameters on one line if you prefer
  camera( 0,  0, -100,  // I'm center on x,y, but 100 far on depth
          0,  0,    0,  // I'm looking at the center of the world
          0, -1,    0); // The y axis is "up" for me.
```

Add that code in the setup, and you should see your sphere straight in the center.


##b) Moving in 3D (without falling...)

Well, we're happy to see our object in their fullest but it's be nice if we could also decide where to put them. In order to move object in 3D, we use the `translate(x, y, z)` function. It takes 3 parameters, each defining how much we move along each axis (horizontal, vertical, depth).

So if we want to display a cube a bit on top:

```java	
  translate(0, 50, 0);
  box(20);
```

First, you'll see that depending on where is your camera, the system is way more sensible than previously. It's not anymore linked with the number of pixel of your screen, but with a real geometry.

Second... If you already tried to display many objects, with many translate, you might see something weird happening. Guess what is happening?
The translate are not forgotten once used. They actually cummulate over time (and reset once you reach the end of `draw()`). There again might sound super weird but ... then again, it is coherent in most usages. In order to precisely place many object, we need to know when to add, and when to discard such translations. This is done with `pushMatrix()` and `popMatrix()`.

In short, `popMatrix()` will discard all changes in your frame of reference seen since last `pushMatrix()`. An example of usage:


```java	 
  pushMatrix();
  translate(0, 0, 0); 
  box(20);
  popMatrix();

  pushMatrix();
  translate(50, 0, 0); 
  box(20);
  popMatrix();

  pushMatrix();
  translate(-29, -20, 50); 
  sphere(20);
  popMatrix();
```


The `translate()` function (and other alike) is best seen as a mofidication of your 3D frame of reference. Your camera doesn't change but your stylus does. If you translate, you translate your whole view. The two matrix functions allow you to save or discard such frame of references.
 
Bonus: not only can you translate, you can also rotate your shapes with three functions. `rotateX(angle)` will rotate your shape along the X axis, like wise for `rotateY(angle)` and `rotateZ(angle)`. Those functions are also being controlled by `pushMatrix()` and `popMatrix()`.
(rotate?)

Remember than you can use these functions with variables too, here is a whole example using all we learned:

```java
int k;

void setup() {
  size(displayWidth, displayHeight, P3D);
  
  // You can put all parameters on one line if you prefer
  camera( 0,  0, -100,  // I'm center on x,y, but 100 far on depth
          0,  0,    0,  // I'm looking at the center of the world
          0, -1,    0); // The y axis is "up" for me.

  stroke(200,30,30,200);
  fill(0,240);
  k =10;
}

void draw() {
  background(255);

  for (int i = -k ; i < k; i++) { // loop over X: 2*k times.
    for (int j = -k ; j < k; j++) { // loop over Y: 2*k times.
    
      pushMatrix();
        translate(i*width/100, j*height/100);
        rotateX(millis() * 0.0005); // Okay, this one is new. millis()
        rotateY(millis() * 0.0003); // count the milli second from start
      
        box(7);
      popMatrix();
    }
  }
}
```


ProTips: your computer will never implode, you're pretty safe at trying to break your code or mess with it. Try to modify fill and stroke color. Like ... put some light shades, high transparency and put a big value to `k` for a surprise. Interesting results sometimes come when you create a system with inner rules, and then push it over its coherency limits.

##c) Using libraries

One last thing before letting you go: using libraries. There is one very simple one that create some arcball kind of camera which is great for visualisation. This library is called peasycam. Lucky for you, it's incredibly simple. In the menu, click on *Sketch->Import Library->Add Library*. Then filter your research by typing "peasycam". Click to install it and bam, you're done. You can look at one example by clicking in the meny on File->Example and moving down to "contributed" library. 

First you need to import the library in your sketch (before you just downloaded it as data) by adding `import peasy.*` on top of your file. Then you need to create a PeasyCam object at the root of your sketch, like you would for any other global object. And last you have to create the object.

You have two ways of doing so. Either the simple `new PeasyCam(this, dist);` which aim the camera at the center of the wolrd (0,0,0). The parameter `this` refers to your sketch (don't fret too much about it, just put `this`) and `dist`, a number defining the distance of the camera from the center.
The longer function reuse some parameters we discussed while defining the `camera()` function: `new PeasyCam(this, lookAtX, lookAtY, lookAtZ, dist);`. Not only do you define the distance, but also where you are looking at.

Below is an example of such camera:


```java
import peasy.*;

PeasyCam cam;

void setup() {
  size(200,200,P3D);
  cam = new PeasyCam(this, 100);
}

void draw() {
  
  rotateX(-.5);
  rotateY(-.5);
  background(0);
  fill(255,0,0);
  box(30);

  pushMatrix();
    translate(0,0,20);
    fill(0,0,255);
    box(5);
  popMatrix();
}
```

But why all the fuss about that library? Well, if you haven't tried already, try to drag and drop (click with your mouse, keep the button pressed, and move around) with your mouse, and see how you can know control your camera!


##d) Oeuf, jambon, fromage
The whole stuff. Armed with new tools and skills, try to imagine how you can port our previous particle system to 3D.

Below is a working solution:

```java	
import peasy.*;

PVector[] p, s, a; //The particles position, speed and acceleration
int k; // The number of particles

PeasyCam cam;
boolean run;

void setup() {
  size(displayWidth, displayHeight, P3D);
  cam = new PeasyCam(this, 2000);
  
  run = true;
  
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
  
  if(run) {
    //background(0);
    //Update acceleration, speed and position   
    for(int i=0; i<k; i++) { 
      a[i].set(0,0,0);
      a[i].add( new PVector( random(-1,1), random(-1,1), random(-1,1) ) );
      a[i].add( new PVector( (0 - p[i].x)/10000, (0 - p[i].y)/10000 , (0 - p[i].z)/10000 ) ) ;
      s[i].add(a[i]);
      p[i].add(s[i]);
    }
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

void keyPressed() {
  
 run = !run; 
}
```

