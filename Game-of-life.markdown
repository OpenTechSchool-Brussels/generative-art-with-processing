---
layout: default
title:  "The Game of Life"
num: 4
---

The material happened to be already super long, so we didn’t want to add that part. It’s completely unsafe. Flee! This section might be updated for *next* time we have the processing workshop. Or might be killed all together. Not sure if it's worth to be added. A little too complexe, not graphic enough. The Game of Life is a fascinating topic, not sure it fit the Generative Art topic well tho (at least not as how explored along the previous logs). Anyhow, here it is.

##o) Cellular automaton: life on your computer##
Gets its inspiration from life. An automaton, governing over the evolution of simple cells with basic rules. Mythical simulation, people think new life form could emerge from it. Other think it’s the rule that govern our world on a lower scale. The basic rule is:

    Rule1: you live if you have at least N1 neighboors on the grid you die if you have at most N2 or at least N3 neighboors on the grid.

What we add is:
    
    Rule2: You average the colors of your neighbours

##a) Setting up our new world##

```java

// MAAAAA code doesn't compile. It's past 2 am, and we told you it was unsafe so ... I'll let it be.

int[][] GofL;
float l, h;
void setup() {
 
  size(displayWidth, displayHeight);
  background(0);
  noCursor();
  noStroke();
 
  int[][] GofL = new int[10][10];
  l = width/10;
  h = height/10;
 
//Create
  for(int i=0; i<10; i++) {
    for(int j=0; j<10; j++) {
      GofL[i][j] = int(random(0));
      rect(i*l,j*h,l,h);
    }
  }


}


void draw() {
  background(0);

//Draw 
  for(int i=0; i<10; i++) {
    for(int j=0; j<10; j++) {
    if(GofL[i][j] == 1) {
          fill(random(255), random(255), random(255), 20+random(150));
          rect(i*l,j*h,l,h);
}
    }
  }
}
```

##b) Life & death##

Explore: Try to make coherent sharing on the edges too.

##c) Granting the cells an identity##
We need to keep the color value some place.

```java

// Can't imagine why this code would compile more. Let's call that inspiration and let it rest. As I should be doing to.

int[][] GofLRed;
int[][] GofLGreen;
int[][] GofLBlue;
float l, h;
void setup() {
 
  size(displayWidth, displayHeight);
  background(0);
  noCursor();
  noStroke();
 
  GofLRed = new int[10][10];
  GofLGreen = new int[10][10];
  GofLBlue = new int[10][10];
  l = width/10;
  h = height/10;
 
  frameRate(4);
 
    for(int i=0; i<10; i++) {
    for(int j=0; j<10; j++) {
      GofLRed[i][j] = int(random(255));
      GofLGreen[i][j] = int(random(255));
      GofLBlue[i][j] = int(random(255));
      rect(i*l,j*h,l,h);
    }
  }
}


void draw() {
  background(0);
 
  //update
 
  //add
  int ii = int(random(10));
  int jj = int(random(10));
  GofLRed[ii][jj] = int(random(255));
  GofLGreen[ii][jj] = int(random(255));
  GofLBlue[ii][jj] = int(random(255));
 
   for(int i=1; i<9; i++) {
    for(int j=1; j<9; j++) {
      
      //Add only if not black, and put black all around
      GofLRed[i][j] = ( GofLRed[i-1][j-1] + GofLRed[i  ][j-1] + GofLRed[i+1][j-1]
                      + GofLRed[i-1][j  ] + GofLRed[i  ][j  ] + GofLRed[i+1][j  ]
                      + GofLRed[i-1][j+1] + GofLRed[i  ][j+1] + GofLRed[i+1][j+1] )/9;
      GofLGreen[i][j] = ( GofLGreen[i-1][j-1] + GofLGreen[i  ][j-1] + GofLGreen[i+1][j-1]
                         + GofLGreen[i-1][j  ] + GofLGreen[i  ][j  ] + GofLGreen[i+1][j  ]
                         + GofLGreen[i-1][j+1] + GofLGreen[i  ][j+1] + GofLGreen[i+1][j+1] )/9;
      GofLBlue[i][j] = ( GofLBlue[i-1][j-1] + GofLBlue[i  ][j-1] + GofLBlue[i+1][j-1]
                       + GofLBlue[i-1][j  ] + GofLBlue[i  ][j  ] + GofLBlue[i+1][j  ]
                       + GofLBlue[i-1][j+1] + GofLBlue[i  ][j+1] + GofLBlue[i+1][j+1] )/9;
    }
   }
 
  //draw
  for(int i=1; i<9; i++) {
    for(int j=1; j<9; j++) {
      fill( GofLRed[i][j], GofLGreen[i][j], GofLBlue[i][j] );
      rect(i*l,j*h,l,h);
    }
  }
}
```

