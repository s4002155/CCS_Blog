---
title: Use for loops to create a grid
published_at: 2024-03-06
snippet: First Homework for S1
disable_html_sanitization: true
---


<iframe src="https://editor.p5js.org/s4002155/full/MG7Twp_rE" width="100%" height="410px"></iframe>

_This is the final result of creating a grid by using a for loop._

# How might I use for loops to create a grid?

![screenshot of existing code](/240306_first_post/existing_code.png)
I started with the code from the sketch that I created in class to use the for loop.

![First attempt at creating a grid](/240306_first_post/first_try.png)
While thinking about how to create a grid using a for loop, the first method I tried was to generate several square codes with adjusted positions.

![Adjusted the scale of the square](/240306_first_post/scale_adjustment.png)
There were two problems with the above method.
1. The size of the square keeps changing
2. The distance between each row is not constant.

The code for the sketch created in class was created so that the scale of the square is adjusted according to frameCount.

However, to create a grid, I need squares with a fixed scale, so the first thing I modified was to change the scale of the squares to **70**.

![Referenced Resources](/240306_first_post/resource.png)
[Source: grid for loop
by cs4all](https://editor.p5js.org/cs4all/sketches/9ADXr9mSx)

Then, to solve the second problem of the first attempt, which was that the distance between each row was not constant, I referred to an example of creating a grid by using the **for loop code**.


![rename to x and y](/240306_first_post/rename.png)
Through the example above, I learned that the **for code** is used to set the setting values for each column and row. So I set column to x and row to y.

But when I ran the code, I got the result **Unexpected end of input**. This was my first time coding or writing code myself, so I was confused as to what to do when I saw results like this.

![for loop definition](/240306_first_post/for_loop.png)
[Source: statement for the for code](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)

Since this error occurred after I modified the for code, I thought that I needed to understand the **for code** in order to fix it.

  While looking at the statement for **for code**, I found the answer in the section *"followed by a statement (usually a block statement) to be executed in the loop"*.

In my code where the error occurred, I used two for codes, but there was only one ***curly bracket*** corresponding to the for code.

![solved the problem](/240306_first_post/solve_problem.png)
After fixing this, the code worked properly again!!!

![The total number of squares has been corrected](/240306_first_post/total_squares.png)
After solving the problem, I began the *grid creation* phase in earnest. First of all, I decided to create a 10x5 grid, so I modified **total_squares** to 50.

![Second problem occurred](/240306_first_post/problem2.png)
And then, I modified the **Square** settings to arrange the 50 squares into 10 rows and 5 columns.

![Adjusted the size of the canvas](/240306_first_post/canvas_size.png)
Due to the existing code where the canvas height was set to 200, the squares did not have enough space, so they appeared to be merged into a rectangle.

Therefore, I modified the canvas size to **368** so that 50 squares are spaced at regular intervals to look like a grid.

![Result of running the code](/240306_first_post/result.png)
A grid is a structure made up of a series of intersecting straight lines. However, the existing color had a strong square color, so it felt like the presence of a square was stronger than that of a straight line. So I finished by changing the **background colour** and **fill colour** to emphasize straight lines rather than squares.

