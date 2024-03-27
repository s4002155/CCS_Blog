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
Then, 'function find_point (start, end, phase)', 'function rand_col ()', and 'function rand_curve ()' were moved to **faller.js** as before.

![re_sketch 1a](/240313_first_HW/re_sketch1a.png)
I deleted unnecessary code from **sketch.js**.

![e_sketch 1b](/240313_first_HW/re_sketch1b.png)
I modified it to 'fallers.push (**new** Faller (bg))' to load the Faller defined with the 'class ()' code in **sketch.js**.

![re_sketch 2a](/240313_first_HW/re_sketch2a.png)
Codes that became unnecessary through the 'fallers.push (**new** Faller (bg))' function were also deleted.

![re_sketch 2b](/240313_first_HW/re_sketch2b.png)
This is the 'function setup()' of **sketch.js**, which has become cleaner than before through the 'class ()' code.

![re_sketch 3](/240313_first_HW/re_sketch3.png)

![re_sketch 4](/240313_first_HW/re_sketch4.png)
Lastly, I finished organizing it by deleting unnecessary code due to the 'class ()' code.


## So what do these mean?
![final sketch code](/240313_first_HW/sketch_final.png)
This is the final look of the code.

![added comments](/240313_first_HW/added_comments.png)
I added code comments to help it be more understandable to humans.
