---
title: Refactor the code to use classes
published_at: 2024-03-13
snippet: First Homework for W2
disable_html_sanitization: true
---

<div align="center">
<iframe src="https://editor.p5js.org/s4002155/full/eU4uh5ShJ" width="100%x" height="442px"></iframe>
</div>

_This is a play scene of Thomas Capogreco's recreated Rafaél Rozendaal's net art piece Falling Falling, by refactoring using class code._

# Which code do I use to refactor?
This net art piece consists of repeating polygons that change color and fall. Therefore, it is effective to use class definitions that can utilize the convenience of objects all at once. Therefore, in the process below, we will reorganize slightly messy and difficult-to-understand code into 'class ()' code.

## working process

![origin code](/240313_first_HW/origin.png)
First of all, in order to use the 'class ()' code, I had to look at the existing code. If you look at the code written in **index.html**, you can see that there are **faller.js** and **sketch.js**.

![sketch.js](/240313_first_HW/sketch.png)
At this time, an object is defined in **faller.js** through the 'class()' code, and repeated objects are loaded through the 'class()' code defined in **sketch.js**.

![faller.js](/240313_first_HW/faller.png)
For this purpose, I first decided to define **_Faller_** using 'class()' code in **faller.js**.

![class faller](/240313_first_HW/class_faller.png)
For a more convenient work environment, I placed **faller.js** and **sketch.js** on both sides so that I could see them at a glance, and then started coding in earnest.

First, to define the code in **sketch.js** as a class, move all the code with faller.@@@ located in the function setup to 'class Faller {} in **faller.js** and then add the code I changed them to this.@@@.

![function draw](/240313_first_HW/function_draw.png)
Then, I moved the code for the polygon into **faller.js**, using the draw function to draw the falling polygon.

_* At this time, I initially used 'function draw()', but I later modified it after realizing that I had to use 'draw ()' code within the 'class()' code._

![function etc](/240313_first_HW/funtion_etc.png)

![re_sketch 1a](/240313_first_HW/re_sketch1a.png)

![e_sketch 1b](/240313_first_HW/re_sketch1b.png)

![re_sketch 2a](/240313_first_HW/re_sketch2a.png)

![re_sketch 2b](/240313_first_HW/re_sketch2b.png)

![re_sketch 3](/240313_first_HW/re_sketch3.png)

![re_sketch 4](/240313_first_HW/re_sketch4.png)


## challenge moment
![problem of the colour](/240313_first_HW/problem_col.png)

![solve the problem of the colour](/240313_first_HW/solve_col.png)

![final sketch code](/240313_first_HW/sketch_final.png)


## So what do these mean?
![added comments](/240313_first_HW/added_comments.png)

add code comments to help it be more understandable to humans
