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

But a `PVector` is not a variable type, it's an object type and hence define an object. Objects don't exactly behave as variables. They store some, so you can access them, but on top of that you have inner functions (called methods), in order to act on them. At first, when imagining an object, you can imagine a human. Variables of the human object could be its name (text variable), its age (int variable) and its height (float variable). Its methods could be "breathing", "running" or "screaming". Beside all that, since we handle a complexe object and not anymore a simple variable, we need to constructe it. This is done by calling a function, called the constructor (which handly has the same name than the type), it handle the whole initialisation of the object.

So, let's review the different possibility of the `PVector` type. Always keep in mind `PVector` is not an object itself, but a type. So the inner variables and methods will be of the instance of this type. Let's see some of the possibilties of `PVector` instances.

```java
PVector p1, p2, p3; // As any other type, we declare our object at the root.

void setup() {
  // We define and initialise it by calling the constructor
  p1 = new PVector();     // By default x = 0 and y = 0;
  p2 = new PVector(1,3);  // When precised, the constructor will take x and y values
  p3 = new PVector(10,10);
}

void draw() {

  // Variables. Accessing them.
  p1.x = 5;
  p1.y = p2.y + p3.y;

  // Method. Using them.
  float distance = p3.mag(); // Return the mag of the PVector, its lenght
  p1.random2D(); // Set p1 as a random 2D vector with a unitary lenght (p3.mag() == 0)
  
  // Unfortunately we can't use classic + - * / operators, we hence need the next methods
  p1.add(p2); // Add p2 to p1
  p3.sub(p2); // Substract p2 to p3
  p1.mult(5); // Multiple both x and y by 5
  p3.div(10); // Divide both x and y by 10
  
}
```

If you want to learn more about PVector methods, you can check their Processing reference pages: http://processing.org/reference/PVector.html. The reference page - http://processing.org/reference/ - is all in all the best ressource to check first or just to read through in order to learn more about the potentials of Processing. If you're wondering why `p1.y = p2.y + p3.y;` can work while we said we couldn't use `+`, it's because here we're not handling the `PVector` but `y`, one of their inner variable, which is a float, and we can use `+` on floats.


##b) Spread and shine##
Let’s look back at the code we wrote in the previous log (i.e.dealing with line, array of variables and random acceleration) and apply it to particles. Try to do it by yourself, or at least to think a bit how you would do that. The following code is one way to do so, in which the particles start from the left, and go toward the right:

```java	
PVector[] p, s, a; //Defines the particles
int k; // Define the number of particles

void setup() {
  size(displayWidth, displayHeight);
  background(0);
  noCursor();
  k = 20; // We want 20 of them apples
 
  // Define the size of the particle array by the number 
  // / of particle we want
  p = new PVector[k];
  s = new PVector[k];
  a = new PVector[k];
 
  // Initialise the acceleration, speed and position arrays.
  for(int i=0; i<k; i++) {
    // Initial position at the left of the screen, with random y
    // To initialise a PVector, we use PVector(x,y)  with values for x and y
    p[i] = new PVector(10,random(height));
    s[i] = new PVector(3,0); // Initial speed toward the right
    a[i] = new PVector(0,0);
  }
}


void draw() {
  //Update acceleration, speed and position 
  for(int i=0; i<k; i++) { 
    a[i] = new PVector(random(0.01)-0.005, random(0.2)-0.1);
    s[i].add(a[i]); // You can’t add vectors together with +
    p[i].add(s[i]); // / to do so, you need to call add.
  }
      
  // Draw the particles
  stroke(255);
  for(int i=0; i<k; i++) { 
      point(p[i].x, p[i].y); // Here we use the point primitive
  }
}
```

In this case, we decided that the particles would go from left to right. You’re not bound to that, you can make them appear anywhere, and move in any direction. From top to bottom while others go from right to left, or even from the center to the exterior. 

But ... we have a little issue here. At some point, our particles will go of the screen. We need a way to give them back some initial position. So, in short it would be: “if you are too much on the right, then you should go back on the left”. There is a keyword that allow you to do so in Processing (and many other languages) it’s if:

```java
if( p[i].x > width) { // if the particles are too far on the right
        //Initialise them anew
    p[i] = new PVector(10,random(height));
    s[i] = new PVector(3,0); // Initial speed toward the right
    a[i] = new PVector(0,0);
};
```

If the condition defines under the parenthesis is right (meaning: equals to true) then we will execute the block of code defined between the braces (the initialisation). We need to have this code working for each particles, so add it up inside the for loop before or after updating the variables.


##b) Of mice and planets IN PROGRESS##
From now, it’s still “experimental”, hopefully everything works, don’t hesitate to call us if it doesn’t.

Until now, the acceleration was random. Let’s put an end to that (more or less…).
In this part, we will make the particle attracted to the mouse cursor.

How do you define a force?
It’s defined by a direction (defined by the point of origin of our force -the mouse- and where it’s applied -the particle), and a value. In our case, the closer the particle is to your mouse, the stronger it is.
You can try other stuff (like the exact opposite to not have a force of attraction, but of repulsion).

In this case, the acceleration is defined by the following lines:

```java
PVector force = new PVector();

    // 1) Get the direction
    force.set( p[i].x - mouseX, p[i].y - mouseY);

    // 2) Get the right value
    //Right now, the further you are, the bigger is the force, we need to invert that.
    // 2.1) Measure the magnitude of the force vector
    float strength = force.mag();    
    a[i].div(strength + strength*strength); // Divide the vector by a value
    a[i].div(-1); // Inverse the vector (to get an attraction vector)
```

If replace our previous rules on acceleration with this one, you should find that our particles are now attracted by the mouse! Move around to test for some neat rendering! And for the astres aficionados try to catch the particles and make them act like comets graviting along your mouse!

Explore:
- Color varying with speed
- try batch with similar speed, similar color. Use many batch, different between batches
- Try to only plot the particles, for instance as rectangle with low transparency.
- Try to not anymore use the mouse as point of attraction but predefined positions, acting as planet. Bonus if you draw the planets.
    

##d) Laws of attraction IN PROGRESS##
Let’s change the acceleration rule. This time the particles are not attracted to the mouse anymore. They are attracted to each other. So basically, for each particle, you need to apply the calculus we did to the mouse, but for other particles.

Try to find out by yourself how it could be made possible, and if you want so clue, this is one possible solution:


```java
//Updating the acceleration for all particles (so don’t put that inside
// / the loop that updates speed and position also)
  PVector tA = new PVector();
  for(int i=0; i<k; i++) {
     a[i].set(0,0);
     for(int j=0; j<k; j++) {
        if(j==i) { // A particle can’t interact with itself
           continue;  // do nothing, continue to the next 
    // / iteration of the for loop
      }
    //get the direction
    tA.set( p[i].x - p[j].x, p[i].y - p[j].y);
    //inverse the power
    tA.div(tA.mag() + tA.mag()*tA.mag());
    a[i].add(tA);
  }
  a[i].div(-1);
  }

//Updating position and speed
for(int i=0; i<k; i++) { 
    s[i].add(a[i]);
    p[i].add(s[i]);
}

//Draw
//As usual..
```


