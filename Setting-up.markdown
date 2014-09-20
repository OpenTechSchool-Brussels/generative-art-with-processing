---
layout: default
title:  "Setting up"
num: 0

---

Let’s get it started.

##a) What is Processing?##
Processing (ou P5) is a programming environment, made by artist, with art creation in mind. It is a set of tools, including a programming language, designed to facilitate the use of software within the visual arts, and to promote visual representations within technology. Processing is focused on making digital creation simple and fun, with an emphasis on visuals and interactions. This makes it particularly fitted for makers, designers and visual artists.

<!--![Alt text](/assets/images/lg_opentechschool.png "Optional title")-->

There are many solution for creating visuals, some more or less close to classical programming language. One of the interesting point of Processing is that it’s a classic programing language. What learn here will help you dwell deeper (if you want) into any other language. Even more, Processing is actually a subset of Java (a classic programing language) so whatever you learn from Java, you can use straight in Processing to buff your creations.

Further more, Processing is an open source language. This means that you have access to the code, and you can do pretty much whatever you want with it. This open source mind is all about sharing, and building together. If you create with Processing, think about releasing your creation in open source so that other people can learn from your work!


##b) Setting up Processing##
To set up processing, just download it : https://www.processing.org/download/

*   Windows: Extract the .zip file you just download anywhere you want (a classic is the Program Files folder, but your desktop will do). Enter the newly extracted folder, and double click on “processing.exe” to start.
*   Mac OS X: Unzip your download file, and drag the Processing icon to the Applications folder (or your desktop if you don’t have the right to the Applications folder). Double-click the Processing icon to start.
*   Linux: Untar your downloaded .tar.gz file and enter the directory you just created. Run processing with the command ./processing.

You should have now in front of you the Processing environment open. It’s similar on all system, so if you share your code, people should have no issue making it run.


##c) Running your first program##
Okay, you’re in front of your command center, now what?
Well, you can see three main zone. On top, the menu. On the bottom, some place for Procesing to give you feedback, especially useful when you’ve messed up something (you will, and part of learning how to code is to learn to enjoy that!). In the center, the main stage where you shine, where you write your code. A processing file is called a sketch.
The menu allow you basic control you can explore by yourself (new, save, open, exit…) sometimes redundant in the icons you can see. Some controls are more specific to Processing, and the two main that will be interested in are run (Triangle shape for the icon, and keyboard shortcut Ctrl/Cmd + R) and stop (Square shape for the icon).

Now that you’re super at ease in this new jungle, let’s actually write something. As mentioned before (maybe), even if you can copy paste the code from this material to your sketch, you shouldn’t. Not only because we love to torture you, but also because you will learn way more this way. You’ll not only remember reading, but remember writing. And you always remember more by doing.

One of the classic first programs one writes is called “hello world”, which basically outputs the text `“hello world”` on your screen. We could do that (`println(“hello world”);`) but the basic output of Processing is graphic not text. So let’s write:

```java
rect(25,25,50,50);    
```

What did it do? If you run that (pressing the icon, “run” in the menu or with your keyboard shortcut), you should see your canvas, with a square in the middle. Kudos, you’re an digital artist! All the next steps are just details. But before you leave full of pride, let us analyse this line.

What you called is a function, and you fed it with parameters, four to be precise. The function is rect and you feed it with parametres in between parenthesis, separated by a comma. So if the function had no parameters, it should be written as `rect()`. You can try to run such a function, Processing will shout at you (gently, but in red) telling you that no, you can’t do that in this house, and that rect is patiently waiting for four parameters. At the end of the line lie a quiet `;`. Its function is to say that this particular command has finished. A common mistake is to forget to put it at the end of commands.


##c) Generative Art##
Generative art refers to art that in whole or in part has been created with the use of an autonomous system. Classic systems can be summed up as a brain and its input/output. For a system that generate art, it means that first the system needs to be fed some information. It needs rules governing the evolution of this input. Last, it has to represent what has been generated.
One can find inspiration for generative art in each of those parts. For instance, what could you feed a generative art program? Very often, it relies on randomness. But you can feed it with a time value, noise, a picture, music…

##d) The code as a medium##
It is important to see code as what it is: a medium that allow for multiple kind of creation, art & design among others. Having a good grasp of what code is allow you to better understand its possibilities and precise your sensibility. Code is a language, a medium, with which you can do many things. You can draw, write poems or sign contracts with a pen. Same with code. And it’s by its practice, its knowledge and the culture you will create that will emerge interesting digital art, design, prototypes... Many thing can be said of the nature of code, and while that would be very interesting to developp, that is out of the scope of this workshop. While that is true, I hope this workshop will make you see how poetic code can be, even if it’s sometimes frustrating: as any deep and complex language is when you are learning it.

