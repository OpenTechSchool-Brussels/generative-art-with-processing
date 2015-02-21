---
layout: default
title:  "Playing with lines"
num: 2
---


One of the rule of generative art could be “draw a lot”. By drawing a lot of simple primitives, you end up with a complex results, not only an accumulation of all elements but also of their relations and interactions.

As the title would let you think, In this section our primitive will be lines. You’ve already learned a lot, don’t hesitate to tweak and to try to apply what you’ve learned along the way.

A line is defined by the two dots it joins. So we need two rules. One for each dots. Let’s start with a simple example, just write the following code in your draw function:

```java 
line(width/2, height/2, mouseX, mouseY);
```

Neat isn’t it? But feeding it with information from the mouse will only create nice results when you have interesting patterns over the mouse. It’ more reactive art than generative art. Let’s solve that side of the problem. 

##o) Random for the win##
Nahh, not for the wine (tho I'll go get some) but for the win. You might think that previous page skills are child's play, but the power of a creator is in how he's using his tools rather on how many or how complexe they are. With a gentle touch, simplest thing as random lines generation can generate feelings, emotions and regulate their evolution over the graphic's span life. Try to explore your sensibility on something as simple as line generation. Once done with it, give a try at the example below, play with it and experiments on the different variations.

```java 
void setup() {
  size(displayWidth, displayHeight);
  background(0, 0, 0);
  noCursor(); noFill(); stroke(255,7); // Yep, as long as you use ";" you can put
                                       //    multiple line of code on the same line
}

void draw() {
  line(random(0,width), random(0,height), random(0,width), random(0,height));
}
```

##a) Random on a frame##
Let’s add constraint on the position of the dots. Let’s constrain them to frames. We can imagine many kind of frames, like rectangles or circle. But in our case we’ll use two horizontal parallel lines. Once you feel at ease with the code, you can try other kind of frames.
A horizontal line is defined by a constant y value (and a vertical line by a constant x value). We promise we’re not lying, but if you don’t trust us, try it out: `line(10, 100, 400, 100);`. This means that both our dots will have constant y value. Only their x value will change, making the dot glide along the frame.

Let’s draw lines between two dots following such rules. Let’s say the first parallel line is at y=100, and the second one is at y = height-100. If we take random x for the two dots defining the line, what would be the resulting code?

```java
line(random(10,width-10), 100,random(10,width-10),500);
```

Might sound a bit twisted and complex at first, but you’ll get a handle on those concepts quickly, and you’ll get into the habit of modeling such system and rules.


##b) Evolving on a frame##
It’s nice to have complete randomness on what you draw, but sometimes you want to have an evolution in your system, rather than doing tabula rasa each time you want to draw something. In order to have such evolution, you need to keep track of some information that you’ll update regularly. In order to store information we use variables. Not the standard variables that have already a meaning and values, but classic variables that we define and to which we give a meaning.

A variable is defined by three things. Its name, what kind of information it stores, and its value. You can store text, integers, float, colors, vectors ... many many things. A complete definition of a variable is as follow: `float myVariable = 20.45;`.

We have in order the variable’s type (`float`), its name (`myVariable`), and the value it’ll be affected (`20.45`). The symbol `=` here doesn’t defines an equality but an affectation. It reads as “let’s calculate what is on the right side of the symbol, and affect the variable on the left with that value”.

Let’s not get too much into details, but if you want your value to be seen everywhere on your program, you need it to be defined globally. For that, you need to define (and not affect) it at the top of your program.

So in our case, we have a line defined by two dots that have fixed y values, and evolving x values. So let’s create two variables, one for each x value. And let’s make it global since we want to see it evolve along the execution of the program.

```java
float x1,x2; // We define the variables

void setup() {
  size(displayWidth, displayHeight);
  background(0,0,0);
  noCursor();

  x1 = width/2+40; // We initialise them
  x2 = width/2-40; // which means we affect them for the first time
}

void draw() {
  stroke(255,255,255,10);
  x1 = x1 + random(-4,4); // We make the values evolve
  x2 = x2 + random(-4,4); //  by adding at each frame a value to them
  line( x1, 100, x2, 500); // We then use the variables to draw the line
}
```

You will see here a strange line: `x1 = x1 + random(-4,4);`. To understand it, you have to remember that when you affect a value, the compute starts calculating what is on the right, not caring to which variable it will affect the value. So first, we compute `x1 + random(-4,4)` and then we affect this value to x1. In this case, it can be summed up as adding `random(-4,4)` to the variable `x1`. Actually, this is such a classic operation that there is a simpler way to write it that emphases on the addition:  `x1 += random(-4,4);`. You’ll see both ways used in this course.

Now that you’re having variable, you can try to tweak the randomness of the value added to the position, or change color, make the color evolve over time (in the same way that you make the position evolves over time). We have already interesting results, but the movement is a bit too mechanic, not smooth enough, not organic.

In the previous section, we randomised the position. In this section, we randomise what we add at each time step to the position. This value added at each time step correspond to the notion of speed in physical modelisation. So in this section we randomised speed. When we aimed at smooth transition (leading to more organic results) we usually don’t command straight in position, or in speed, but in acceleration (the speed of speed). Which means that at each step, we add the acceleration to a speed variable, and the speed variable to the position value. Who would have come to this workshop if they knew that not only you’d be learning maths, but also physics?!

So in the end, we need new variables to represent the acceleration. Create those variable globally (like x1 and v1) and initialise them to 0 (we’re starting with no acceleration. Then, since acceleration is the speed of speed, we will just add acceleration to the speed, at each execution of the draw function. For the first dot, with a random acceleration represented by the variable a1, the whole system will look like:

```java
a1 = random(-1,1);
v1 += a1; 
x1 += v1;
```

Get this behavior working for both dot, and you’ll be in for a beautiful surprise!

But you’ll realise that a random acceleration means that things go out of hand (or screen in our case) pretty fast. Let’s … well, tweak randomness. On top of that randomness, let us have an acceleration that goes toward the center when you’re far from it. For that, we need two things. A value that is positive on the left (so that you'll go toward the right, hence center) and negative on the right (hence toward the left, and the center). Secondly, we need a value that is low when close to the center (not much impact) and gets bigger when you're far from it (big impact).

Lucky us, the position `x` seems to fit that almost perfectly. The more on the right, the higher the value, the more on the left, the higher the negative value. You already see that we have the opposite sign we want (on the left, position is negative, but we want a positive force), so let's use `-x`. Unfortunately, `-x` equals zero on the far left of the screen, not at the middle of the screen (which is `width/2`). We need to make a translation and hence use `width/2 - x`.

```java
a1 = random(-1,1)    // the random part
   + (width/2 - x1);  // the “please come back to the center” part
```

One last thing is needed now. When you used `random(-1,1)` for the acceleration, it worked well enough. Higher value meant a berserk acceleration. So values (negative or positive) that has a strenght of 1 seem to be good. What would be the strenght of `(width/2 - x1)`? Imagine your screen has a width of around 1000, if your line is at the edge, it means ... a value of acceleration of 500! Quite too much. You just entered by the front door the glorious world of parametre optimisation. We need to tweak the value to a better range. There is no perfect range, different ones will imply different behaviors. It's up for you to chose the one you want, for me 3000 worked well enough. 

```java
a1 = random(-1,1) + (width/2 - x1)/3000;
```
##c) Looping

Computing is all about automatisation. Drawing rectangles one by one is nice but sometimes you want to repeat one part of your code many time, only with slight variations (like ... based on a counter). You can either rewrite many times your code (not only a lenghty process, but an error prone one when you need to update it) or use a new structure: the for loop:

```java
// Don't sweat too much over it, the next paragraphs explain it all
  stroke(255,10);
  for(int i = 0; i < 1000; i = i + 1) {
    line( 10 + i, 100, 10, 10);
  }
```

So, what is such block of code doing? A for loop will repeat a block of code until a condition is met. It can be understood in English as: "First do something (the initialization). Then repeatedly execute code (the block of code) until I decide you’re finished (the condition). Each time you have finished executing the code between braces, do one thing in particular (usually an iteration over a counter)".

To be more precise, a for loop is defined by 4 components:

* First the *initialization*, here `int i = 0;`. We define and instantiate here a new variable. Not a float, but an integer. We saw this type earlier with relation to colors. An integer is defined by its type: int, it is a variable with no fractional part, no numbers after the coma.

* Then you have the *condition*, here `i < 1000`. A condition is something that is true or false. In our case, we use the mathematical symbol < to check if a value is inferior to another one. Other symbol allow for different test (such as > for superior to, or == to test the equality. Not to be confused with = for affection, a classic mistake.)

* Then you have the *update*, here (as often) an iteration over an index: `i = i + 1;`.

* Last,  you have the *block of code*, located between braces `{ }`, that is executed by the for loop.

Let's get back to our previous code:

```java
  for(int i = 0; i < width/2; i = i + 1) {
    line(0,0,2*i,height/2);
  }
```

The code drawing lines will be executed repeatedly with values of i from 1 to width/2. Changing the value of i will change the offset of the x position. We should hence see a serie of lines along the x axis.

But wait, that's not all! You can even nest loops; don't mess up the indexes on each loops tho.

```java
// Ok, not really lines, but so 80's....

void setup() {
  size(displayWidth, displayHeight);
  background(0);
}

void draw() {
  for (int i = 0; i < width/40; i = i + 1) {
    for (int j = 0; j < height/40; j = j + 1) {
      fill(random(255), random(255), random(255));
      rect( 10 + 40*i, 10 + 40 *j, 10, 10);
    }
  }
}
```

##d) Handling multiple Lines##
Hmm, looping is nice, but we lose all the gorgeous animation we had... We want our lines to have a behavior. For that, we need many variables. We could define a heck load of them (x1_0, x1_1, x1_2 ...) but that’s not really the way to do it. Programming is all about simplifying, automating and organizing. When we need to store multiple variable, the commonest data structure is the array.

An array is just a list of variables, indexed over a integer. If you define an array of ten elements, you can ask it to give you its fifth element:

```java
    float[] ArrayOfFloats = new float[10]; // Defines an array of floats, of size 10.
    float rez = ArrayOfFloats[4]; // Access to the fifth value.
    ArrayOfFloats[5] = 4; // Modify one of its value.
    int size = ArrayOfFloats.length; // Size of the array

```

No, there was no mistake in the writing (not this time at least), the arrays index start at 0, not 1. So if you call `arrayOfFloats[1]`, you will not get the first element, but the second. This is why to call the fifth value, we need `arrayOfFloats[4]`.


When you want to access or modify the value of each element of an array, you could call them one by one but... that wouldn’t be very simple or automated would it be? We need a way to create a variable that would go from 0 to the size of the array... how could we do that? Yep, with a for loop. Let's imagine we want to fill an array with zero value at start, and then add random values to each of its cells. An array is a complexe variable but still a variable. All you learnt about variable (declaration, definition, initialisation...) can be applied to arrays. So this would look like:


```java
// Declare the variable/array at root for it to be used globaly (i.e. always remembered)
float[] arrayOfPositions; // Defines an array of floats, of size 10.

void setup() {
  size(displayWidth, displayHeight);
  background(0);
  stroke(255,10);

  //Define it in setup
  arrayOfPositions = new float[10];

  //Initialise it in setup
  for(int i=0; i<10; i+=1) {
    arrayOfPositions[i] = width/4;
  }

}

void draw() {  

  //Use it in draw
  for(int i=0; i<10; i+=1) {
    arrayOfPositions[i] += random(-8, 10);
  }

  //And display

  for(int i=0; i<10; i+=1) {
    line(arrayOfPositions[i], 0, arrayOfPositions[i], height);
  }

} 
```

So, you already automated a bit of the task, but there is still one repetition... That 10 is mentionned twice. An array should know its length right? Well, lucky you, in our case it does. In order to call a variable internal to an object (or a function for that matter) you need to use the `.` operator. The internal variable corresponding to the length of the array is called ... length. Good. So if you want to apply that to our previous call, you'd write `arrayOfFloats.length`. Go ahead, try to replace `10` by that new variable in the `for` loop. 

Ok, now we know how to use array (did you already think of creative to use your new powers?). Let’s use them to have maaaaany lines. First, as for other variables, we need to define those arrays globally. Then whatever calculus we made on our previously separated variables, we’ll do on each element of the array. This might be a bit hard, but try already by yourself to reorganise your code. You can have a pick at the following way to do so if you’re stuck. If you end up going straight to the answer, be sure to experiment with it enough to be sure that you understand each part of the code.

```java
int k; //Will parametrise the number of lines
float[] x1,x2,v1,v2,a1,a2; // You can instantiate many variable at once 
                   //  / when they have the same type. Just
   //  / separate them with a comma
void setup() {
  size(displayWidth, displayHeight);
  background(0);
  noCursor();

  k = 10; // We want 10 lines 

  // You can put many command on a same line
  x1 = new float[k]; v1 = new float[k]; a1 = new float[k];
  x2 = new float[k]; v2 = new float[k]; a2 = new float[k];

  // Initialise acceleration, speed and position
  for(int i=0; i<k; i++) { // i++ is the same as i+=1 or i=i+1
  
    a1[i] = random(-1,1) + (width/2 - x1[i])/3000;
    a2[i] = random(-1,1) + (width/2 - x2[i])/3000;
    
    v1[i] = 0;
    v2[i] = 0;
    
    x1[i] = width/2;
    x2[i] = width/2;
  }

}


void draw() {

  //Updating acceleration, speed and position
  for(int i=0; i<k; i++) {
  
    a1[i] = random(-1, 1) + ( (width/2-x1[i]) /3000);
    a2[i] = random(-1, 1) + ( (width/2-x2[i]) /3000);

    v1[i] += a1[i];
    v2[i] += a2[i];

    x1[i] += v1[i];
    x2[i] += v2[i];
  }

 //drawing the lines
  stroke(255, 255, 255, 20);
  for(int i=0; i<k; i++) {
    line( x1[i], 100, x2[i], height-100);
  }

}
```

