---
layout: default
title:  "Getting to know your canvas"
num: 1
---

Welcome soldier, you’ve done already so much, and yet your country await more for you. In this section (guess what) you’ll learn about the canvas, and how to draw. Learn, prosper, and spread the visuals!

##o) the coordinate system##
So, tough luck, here no pencil, if you want to draw something, you’ll need to use …. maths. Well, at least numbers.
You will draw using coordinates. Basically, your screen as a grid, full of pixel. In order to pinpoint to one particular pixel, you need two informations: at which height of the screen it is and at which width of the screen. Those are coordinates, symbolised as the couple (x,y), x on the horizontal axis, and y on the vertical one. This is in the end a classical two dimensional system. The origin (x=0 and y=0) is on the top left corner of your screen. Positive x goes toward the right, and positive y goes toward the bottom of your screen. Yep, a bit confusing.
It’ll all make sense (or at least a bit more) when you’ll start drawing shapes. And guess what, it’s the next section!


##a) Drawing primitives##
Yes it is. In computer graphics, the basic items that you can draw are called primitives. They range from the basic (dots, lines, rectangles) to the complexe (cubes, spheres) to the esoteric (tea pot, monkeys… depending on the software/language you’re using).
In our case, we’ll focus with simple ones: mainly dots, lines & rectangles. If you remember, you already know how to draw a rectangle: `rect(25,25,50,50);`. Now, what could mean these parameters? One way to find out, which will work in all case is to explore. Change the value, and see what happens. You’ll discover that you’re feeding the function with the position of the rectangle, and its height and width following : `rect(xPosition,yPosition,width,height);`. If you can’t remember if first come width or height, it’s easy, it’s always the x (horizontal) related information that comes first. Note that the position of the rectangle doesn’t define its center, but it’s upper left corner. That’s life. (Actually some tweaking allow you to change that, but that’ll be for another lesson.)

You have other functions for other primitives, such as `point(xPosition, yPosition);` that allows you to draw a dot a precise position on screen. A segment is a line that links two dots, implying that you need to give two positions on screen: `line(xPos1, yPos1, xPos2, yPos2);`. If you want to draw an ellipse, you can, by specifying its position and how large and tall it is: `ellipse(xPos, yPos, width, height);`. Note that here the position defines the center of the ellpise, not it upside left corner. Can you imagine how you can draw a circle using this function? (same than drawing a square from the rect function).


Here an example of code to sum up all primitives we’ve seen:

```java
line(10,10,10,90);
rect(8,48,44,4);
line(10,50,50,50);
line(50,10,50,90);
line(75,50,75,90);

ellipse(75,25,10,10);
point(75,25);
```
Even if basic, you’ve learn a few tools that allow you to express yourself. Why don’t you try to make a little monster’s face out of these shapes?


##b) Colors##
So, now you know to draw, let release the full spectrum of your creation by adding colors! Processing allow you many way to play with colors but we’ll settle with the basic one: the classic separation of color in four components: Red, Green & Blue (or RGB), over which we’ll add transparency (or alpha). Each component is an integer (a number with no value after the comma,  no fraction part, no decimals; such as 0, 3, 34 or -20) between 0 and 255. In processing, the type that is linked with integer is called `int`. We will learn more about it later.

You have three main way to apply color. First you can apply colors along the edge of your shape, second you can apply it inside the shape, or you can lastly apply it to the background.

First let’s play with the background, easiest way to test out colors. In order to modify the background colors, just call `background(Red, Green, Blue);`. For instance for a Red background: `background(255,0,0);`. How would you create a black or a white background ? Hard enough to find the Red Green Blue values for clean colors, but what about ... teal? Lucky you, Processing put a color selector in the IDE. Just click in the menu on Tools, then Color Selector.

Now let’s apply those colors to the shapes we created earlier. For that we have two functions, which are used in the same way: `stroke` and `fill`. Stroke define the color we will use from now for the edges of the primitives, and fill defines the color we’ll use for now for the inside of the primitives. We use it the same way as background, with the added parameters of transparency: `stroke(Red, Green, Blue, Alpha); fill(Red, Green, Blue, Alpha);`. In case you don’t want any stroke or any fill then you can call respectively `noStroke()` and `noFill()`. For instance: 

```java
background(255, 0, 220);
stroke(200, 100, 100, 255);
fill(50, 10, 200, 40);
rect(25, 25, 50, 50);
stroke(100, 200, 100, 255);
ellipse(70, 70, 40, 40);
noFill();
ellipse(70, 25, 20, 20);
```
Remember, if you want your shape to be totally seen, with no transparency, it means you want an alpha to be maximum (in our case, 255).

Did you try to draw a face in the previous section? If so, it’s time to add color to it!


##c) FullScreen & size of canvas##
True, we released the full spectrum of your creation. But... it can’t leave in such small canvas! It needs something bigger, and we’re here to grant it.
First let us modify the size of the window. For that, we use the function `size(width,height);`. As you’ll have guessed, width & height define the ... width & height of your application’s window.

Running your application in fullscreen is called presenting it, in the Processing lingo. To present your sketch, you can either call the command from the menu, or use a keyboard shortcut: Ctrl/Cmd + Shift + R. Yep, you just add Shift to the Run keyboard shortcut.

Now you need to have a window with a size fitting your screen to have a true full screen. The way to do it is to call some variables that have a predefined value in Processing. We’ll learn more about variables later on. Those variable are `displayWidth` & `displayHeight`. They refer respectively to the width of your current screen in use, and to its height. So, who you’re gonna call? No, not ghostbusters, but the size function, with those two variables as parameters: `size(displayWidth, displayHeight);`.

Now you can contemplate your creation in its full glory.

On a side note, every piece of code you write has an impact. But sometimes you want to just add comments, in order to put in perspective what you just wrote. For that we use special code, called comments, that is ignored when you run your program.

You can define your comment in two ways:

```java
 // This is a comment on one line

/* this is 
a comment
on multiple
lines */
```

##d) Your first superpower: Randomness##
Now things are getting serious. Random seems at first … well, random, but there is way much more to it. Lucky you, random is awesome. Or should I say, it’s seen as awesome. What makes Generative Art more or less like a legal LSD is that the human brain is wired to search and find patterns (like when you look at clouds). So when you will show chaos, non organise mess, the brain will try to make sense of it and the spectator will see patterns. Call that co-creation. Yep, that’s fascinating.

In Processing, the basic function for randomness is the lengthy but well named `random()` function. Calling the random function will return you a floating number. A `float` is a number with a fraction part, such as 1.34, 10.567 or -13.00. You can call it in three different ways:

```java
random(); // returns a float between 0 and 1
random(max); // returns a float between 0 and max
random(min, max); // returns a float between min and max
```

Whenever you put values, would that be for the size or position of primitives, for colors, or for the size of your window, you can put random numbers. For instance, a rectangle with random color would be:

```java
fill(random(255), random(255), random(255), random(255));
rect(25,25,50,50);
```

Try to run multiple times your sketch to see what happens to your results. You will see that if randomness is awesome, controlled randomness is sometime better.

If you want to refer to the size of your windows, and not the resolution of your screen, then you can use two standard variables in Processing: width & height. So if you want a rectangle appearing at a random place in your screen:

```java
fill(random(255), random(255), random(255), random(255));
rect(random(width), random(height),50,50);
```

Try to add a few rectangles by repeating that last line, and see how they color merge depending on the alpha value you use. You can already realise that some range of alpha create better results than others.


##e) Adding dynamism##
I feel you. You want more. After all, this canvas is supposed to be modular, why are we keeping it static? Where is the life? Well, life is in this section.

There are two ways to program in Processing: the one we did, in which the program follow a chronological line, from top to bottom, and then finish. Then there is another way, that allow repetition in the behavior. This is the common way to code in Processing. In order to use it, we degine two standards functions: setup and draw. The setup function is called once, a the start of the program and after that, the function draw is called repetitively, as long as the program run. Here is the default look of your next program:

```java
void setup() {
    //What the function is supposed to do
}

void draw() {
    //What the function is supposed to do
}
```

We define here two functions. A function is defined by what it does, what you feed it (input) and what it return (output).
    The type of returned value is defined before the name of the function. In our case it’s void, meaning that it doesn’t return anything. As in our previous functions, we define the parameters (input) between parenthesis. We have none there. So no input and no output. The code that the function will execute is located between the braces { }. Those braces in general define what we call a block of code. It’s there that you will put the kind of code you wrote in previous sections.

Let’s use this new formalism to add regularly rectangles:

```java
void setup() {
  size(displayWidth, displayHeight);
  background(0,0,0);
}

void draw() {
  fill(random(255), random(255), random(255), random(255));
  rect(random(width), random(height), random(100), random(100));
}
```

Yay! But there could be a few tweaking… Let’s get rid of the stroke color, and let’s get rid of that annoying cursor. For that, call in the setup function `noStroke()` and `noCursor();`.
Now that’s better.
Even with such simple primitives and behavior, you can already create complex results. Try to tweak the value of alpha to see how to mix best the primitives. And you can also play on the canvas as a whole. Let’s get some shading over time by adding at the start of the draw function the following code:

```java
  fill(0, 0, 0, 20);
  rect(0, 0, width, height);
```

By adding black with a very low alpha, we can simulate a fading off of the drawing. Try to explore other possibilities with the tools you already have at hand.


##f) Interacting##
There are many ways to interact with Processing, would that be with your keyboard, your mouse, your mic, your camera, your smartphone, your Arduino, your ... ok you got it, with almost anything. This workshops doesn’t make an emphases on interaction, but it doesn’t mean you can’t add it on the side.

In this section, we’ll discover another Processing standard function that is triggered each time you press a key on your keyboard: keyPressed.
To sum up:
- setup is only called once, at the begining
- draw is called endlessly (unless asked otherwise) after setup 
- keyPressed is only called when you press a key on your keyboard
- and as a bonus, guess what does the function mousePressed?

In order to use that function, you define it the same way you did for setup  and draw. Just write outside of any other function:

```java
void keyPressed() {
   //Do something when the key is pressed.
}
```

Whatever code you'll put there (drawing something, changing a color, calling other functions etc. etc.), it'll be executed when you press a key. Now of course, you'll want to have more precision in the selection of the key. That requires some stuff we'll see later on in the workshop (even more that the emphase here is more on generative art than interactive art, that last part will be for another workshop!). One function that you can call by the press of a button that will be pretty useful is the `saveFrame(nameOfFile)` function. The name says it all: it save the frame as a picture in a file you decide the name of. For instance, if you want to save what is displayed on your Processing window each time you press a key:

```java
void keyPressed() {
 saveFrame("output.png"); 
}
```

Unfortunately here the name is always the same. If you want save multiple frames like output-001.png, output-002.png, ... modify the function as follow: `saveFrame("output-###.png");`.

##e) Looping##
Computing is all about automatisation. Drawing rectangles one by one is nice but sometimes you want to repeat one part of your code many time, only with slight variations (like ... based on a counter). You can either rewrite many times your code (not only a lenghty process, but an error prone one when you need to update it) or use a new structure: the for loop:

```java
// Don't sweat too much over it, next paragraphes explain it all
for(int i = 0; i < 100; i = i + 1) {
 rect( 10 + 40*i, 100, 10, 10);
}
```

So, what is such block of code doing? A for loop will repeat a block of code until a condition is met. It can be understood in english as: "First do something (the initialisation). Then repeatedly execute code (the block of code) until I decide you’re finished (the condition). Each time you have finished executing the code between braces, do one thing in particular (usually an iteration over a counter)".

To be more precise, a for loop is defined by 4 components:

* First the *initialisation*, here `int i = 0;`. We define and instantiate here a new variable. Not a float, but an integer. We saw this type earlier with relation to colors. An integer is defined by its type: int, it is a variable with no fractional part, no numbers after the coma.

* Then you have the *condition*, here `i < 100`. A condition is something that is true or false. In our case, we use the mathematical symbol < to check if a value is inferior to another one. Other symbol allow for different test (such as > for superior to, or == to test the equality. Not to be confused with = for affection, a classic mistake.)

* Then you have the *update*, here (as often) an iteration over an index: `i = i + 1;`.

* Last,  you have the *block of code*, located between braces `{ }`, that is executed by the for loop.

Let's get back to our previous code:

```java
for(int i = 0; i < 100; i = i + 1) {
 rect( 10 + 40*i, 100, 10, 10);
}
```

The line drawing a rectangle will executed repeatedly with values of i from 1 to 99. Changing the value of i will change the offset of the x position (`rect( 10 + 40*i, ...`). We should hence see a serie of cube along the x axis.

But wait, that's not all! You can even nest loops; don't mess up the indexes on each loops tho.

```java
for(int i = 0; i < 100; i = i + 1) {
 for(int j = 0; j < 100; j = j + 1) {
  rect( 10 + 40*i, 10 + 40 *j, 10, 10);
 }
}
```

Try to add little colors to such display and you'll get back in the 80's in a matter of seconds.

Some time you only want repetition, with no variations (i.e. not using the evolving counter in the block of code inside the loop). We'll finish this chapter on a full course meal with such repetition. You should know everything there but one thing: `mouseX` and `mouseY`. They are standards variable, already defined and handled by Processing. As expected, they respectfully give you the position of the cursor in your canvas in x and y.


```java
void setup() {
  size(displayWidth, displayHeight);
  background(0, 0, 0);
  noCursor();
  noStroke();
}

void draw() {

  // Shadows are coming!
  fill(0, 0, 0, 5); // Bahhh, Processing keep an ugly grey when alpha is too low :(
  rect(0,0,width, height);
  
  for(int i=0; i<5; i++) {
   fill(random(255), random(255), random(255), random(255));
   rect(mouseX + random(-20,20), mouseY + random(-20,20), random(2,5), random(2,5));
  }
  
}

void keyPressed() {
  // For the museums
  saveFrame("output-###.png");
}

void mousePressed() {

  // Add a new rectangle when you click
  fill(random(255), random(255), random(255), random(255));
  rect(mouseX, mouseY, random(100), random(100));

}
```
