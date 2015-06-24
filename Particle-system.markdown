---
layout: default
title:  "Particle system"
num: 3
---

Let’s up the level a bit more. Particle system were made possible with hardware being more and more powerful. You can simulate quite complex behavior (fire, smoke, liquids…) or just use them to have fun, which will be our case. It can be pretty process intensive (difficult for your computer to compute it quickly) so don’t start straight with a million particles!

##o) What is a particle system?##
You’ll never guess. It’s a system with particles inside. Particles are physical objects with a position, speed and acceleration. They can be represented as you see fit (would that be individual shape, trajectory or links between them) and can (or not) interact with each other. Usually you don’t have one or two, but closer to hundreds or even more than millions in complex simulation. In a particle system, the emphasis is not on the individual particles, but on what they create as a whole. This is pretty fitting for Generative Art. You search particle system on youtube, you’ll find quite mesmerizing visualisation. And once you’ve done yours, don’t hesitate to upload it too :D

##a) Object, variables, methods & PVector##
If before we had dots moving alone a frame, with only `x` evolving, now we have the whole deal: `(x,y)`. While we could treat each information independently (at the cost of repeted code, implying more energy & time spent, and errors) we can see them as a whole, as a complexe variable, called an object. There are many kind of object, in our case, this one is called a `PVector` (P for processing, Vector for ... vector). As such, it defines a new type of variable. It can be used to store 2D or 3D data, in our case we'll only take care of 2D vectors.

But a `PVector` is not a variable type, it's an object type and hence define an object. Objects don't exactly behave as variables. They store some, so you can access them, but on top of that you have inner functions (called methods), in order to act on them. At first, when imagining an object, you can imagine a human. Variables of the human object could be its name (text variable), its age (int variable) and its height (float variable). Its methods could be "breathing", "running" or "screaming". Beside all that, since we handle a complex object and not anymore a simple variable, we need to construct it. This is done by calling a function, called the constructor (which handily has the same name than the type), it handle the whole initialisation of the object.

So, let's review the different possibility of the `PVector` type. Always keep in mind `PVector` is not an object itself, but a type. So the inner variables and methods will be of the instance of this type. Let's see some of the possibilities of `PVector` instances. The upcoming code has no specific aim but to show you how `PVector` are working.

```java
PVector p1, p2, p3; // As any other type, we declare our object at the root.

void setup() {
  // We define and initialise it by calling the constructor
  p1 = new PVector();     // By default x = 0 and y = 0;
  p2 = new PVector(1,3);  // When precised, the constructor will take x and y values
  p3 = new PVector(10,10);
}

void draw() {

  // Here how you can access each separate Variables.
  p1.x = 5;
  p1.y = p2.y + p3.y;

  // Here are some useful methods.

  // Setting both values at the same time
  p1.set(42, 42);
  
  // Return the mag of the PVector, its length
  float distance = p3.mag();
  
  // Set p1 as a random 2D vector with a length of 1
  p1.random2D(); 
  
  // Unfortunately we can't use classic + - * / operators.
  // Instead, we use the next methods
  p1.add(p2); // Add p2 to p1
  p3.sub(p2); // Substract p2 to p3
  p1.mult(5); // Multiple both x and y by 5
  p3.div(10); // Divide both x and y by 10
  
}
```

If you want to learn more about PVector methods, you can check their Processing reference pages: http://processing.org/reference/PVector.html. The reference page - http://processing.org/reference/ - is all in all the best resource to check first or just to read through in order to learn more about the potentials of Processing. If you're wondering why `p1.y = p2.y + p3.y;` can work while we said we couldn't use `+`, it's because here we're not handling the `PVector` but `y`, one of their inner variable, which is a float, and we can use `+` on floats.


##b) Spread and shine##
Let’s look back at the code we wrote in the previous log (i.e. dealing with line, array of variables and random acceleration) and apply it to particles. Try to do it by yourself, or at least to think a bit how you would do that with your new skills. The following code is one way to do so, in which the particles start from the center and evolve toward the exterior of the screen:

```java	
PVector[] p, s, a; //The particles position, speed and acceleration
int k; // The number of particles

void setup() {
  size(displayWidth, displayHeight);
  background(0);
  noCursor();
  k = 20; // We want 20 of them apples
 
  // Particle array size is the number of particles we want
  p = new PVector[k];
  s = new PVector[k];
  a = new PVector[k];
 
  // Initialise the accelerations, speeds and positions.
  for(int i=0; i<k; i++) {
    p[i] = new PVector(width/2, height/2); // Center screen
    s[i] = new PVector(0,0);
    a[i] = new PVector(0,0);
  }
}


void draw() {
  //Update acceleration, speed and position 
  for(int i=0; i<k; i++) { 
    a[i] = new PVector(random(-0.1,0.1), random(-0.1,0.1));
    s[i].add(a[i]);
    p[i].add(s[i]);
  }
      
  // Draw the particles
  stroke(255);
  for(int i=0; i<k; i++) { 
      point(p[i].x, p[i].y); // Here we use the point visual primitive
  }
}
```

Soooooo pretty. Try with many many particles and ... of course, transparency :D


##c) Of mice and planets##
Soooo pretty, but soooo off the screen. We have the same issue than previously with our lines. And guess what? We'll solve it the same way! Only difference is that now we're in 2D so what we did on `x` as a float, we'll do on `(x,y)` as a PVector. This time, let's make the particles attracted by the mouse cursor so that we can play with it. Don't hesitate to put other positions (such as the centre of the screen, as we did for the lines).

```java
  // A full line, but take your time and you'll understand it.
  // So full that it was break on two lines for better readability
  a[i].set( random(-0.1,0.1) + (mouseX - p[i].x)/9000,
            random(-0.1,0.1) + (mouseY - p[i].y)/9000);
```
In this log, we discover new graphic directions and keep it simple. It doesn't mean that you have to keep it simple too,you can & should explore, for instance you can try:
- Color varying with speed
- Batch of particles with similar speed, similar color. Launch at the same time different batches.
- Try to only plot the particles (not their trajectories, by using `background(0);` at the beginning of draw). Give them another graphic primitive (`ellipse(p[i].x, p[i].y,5,5);`). Set it up nice `noStroke(); fill(255,10);`. And try with many many particles!
- Try to not anymore use the mouse as point of attraction but predefined positions, acting as planets. Bonus points if you draw the planets.
- And many many others...
    
##e) Connect and reject##
One possible exploration was so nice people lobbied to have it included. We can display the particules ... but we can also display their connexions, and that's awesome. For once we won't touch the update part of the code, but the display. We used to draw as:

```java
  // Draw the particles
  stroke(255);
  for(int i=0; i<k; i++) { 
      point(p[i].x, p[i].y); // Here we use the point visual primitive
  }
```

Now, we'll just draw the particles as ellipse, and lines between each of them. In order to draw the lines, we'll need to go through the particles array twice nested, once for the particle at one end of the line, once for the particle at the other end of the line. For the most acute, you'll see we made a little redundancy in the code below for simplification purpose. (Oh, and don't push up too high the number of particles...)

```java
  background(0);
  
  // Draw the particles
  noStroke();
  for(int i=0; i<k; i++) { 
      fill(255);
      ellipse(p[i].x, p[i].y, 5, 5);
      fill(255,30);
      ellipse(p[i].x, p[i].y, 30, 30);
  }
  
  //Draw the links
  stroke(200);
  for(int i=0; i<k; i++) {
    for(int j=0; j<k; j++) { 
      line(p[i].x, p[i].y, p[j].x, p[j].y);
    }
  }
```

That's nice but ... the lines make it feels more mathematics than organic. Let's not always display the lines, let's do that only if particles are close enough. Ahhh at last, the ultimate computer keyword, summing up all that is a computer : `if`. Tests. And actions that follows depending on the answer, that's the basic of computing, it was high time we got there!

An `if` structure allow you to make decisions. At its most complete it is separated in three parts. If it's raining (condition) I'm staying in (action to do if condition is true) else I'm leaving (action to do if condition is false). In code you have it this way:

```java
 if(age < 18) { // Forbidden to enter
    fill(255,0,0);
 } else { // Free to enter
    fill(0,255,0);
 }
 
 ellipse(width/2, height/2, 100, 100);
```

In our case, we want to draw the line only if the particles are close enough. Let's just make a test before calling the line function. Remember from previous code that the length of a `PVector` is accessed by its `mag` method.

```java
  //Draw the links
  stroke(200);
  for(int i=0; i<k; i++) {
    for(int j=0; j<k; j++) { 
    
      PVector diffPos = p[i].get(); // the get method return a copy of the vector
      diffPos.sub(p[j]);
      if(diffPos.mag() < 50) {
        line(p[i].x, p[i].y, p[j].x, p[j].y);
      } // We do nothing if condition is not met, so no need for the "else" part
      
    }
  }
```

##e) Laws of attraction##
Enough already with the particles!! .... One last thing? Ok, one last. This time let's focus on the update part, the behavior of the particles. Up to know, they were attracted to the mouse cursor or to static positions. A particle really gets neat when particles interact with each other. We had that with graphism (the lines). Now we'll have it in their behavior by making them attracted by each other. In short, for each particle, you need to apply the calculus we did to with the mouse position, but now to all the other particles' position. Some for loop in the making...

Try to imagine or even code it yourself. But if you're curious, here is one possible solution (you'll see that in it, we separated the update loop in two. One part specially for the acceleration update, and then for both the speed and position). Here, getting the right acceleration is a more complex process, so we start from zero, and add up until we have the right value. Up to you to check back the parameters and see which are the most fit.

```java
  //Updating acceleration
  for(int i=0; i<k; i++) {
    // Initialisation at zero
    a[i].set(0,0);
    
    // Force between particles
    for(int j=0; j<k; j++) {
      a[i].add( new PVector( (p[j].x - p[i].x)/15000, (p[j].y - p[i].y)/15000) );
    }

    // Random force
    a[i].add( new PVector( random(-0.1,0.1), random(-0.1,0.1) ) );

    // Force that pulls you toward the centre
    a[i].add( new PVector( (width/2 - p[i].x)/9000, (height/2 - p[i].y)/9000 ) );
  }

  //Updating position and speed
  for(int i=0; i<k; i++) { 
    s[i].add(a[i]);
    p[i].add(s[i]);
  }

```

Ok, time to tell you the truth... It's not working like that in the solar system, or any mass based system... All the forces we applied were following one pattern: the further you were, the stronger you were pulled back. It's not the case with planets. It's more like the opposite. The closer they are, the stronger they are pulled together. For now I'll let you that as an exercise!
