---
title: How closely I can replicate Rafaël Rozendaal's work?
published_at: 2024-03-10
snippet: Seconde Homework for S1
disable_html_sanitization: true
---


<iframe src="https://editor.p5js.org/s4002155/full/B-xV42n_Y" width="1000px" height="642px"></iframe>

_This is the end result, what I copied Rafaël Rozendaal's work as closely as possible._

# Which work by Rafaël Rozendaal did I choose?
![FlyingFrying
by Rafaël Rozendaal](/240310_second_HW/FlyingFrying.png)
[Source: FlyingFrying
by Rafaël Rozendaal](https://www.flyingfrying.com/)

Among Rafaël Rozendaal's various works, I chose **frying flying .com**, created in 2014. The main feature of this work is that it looks like fried eggs flying in the air.

## Work Process
![start coding](/240310_second_HW/start.png)

First of all, I created a new sketch file to replicate Rafaël Rozendaal's work.

![changed canvas setting](/240310_second_HW/canvas.png)

I resized the **canvas** to a similar size to Rafaël Rozendaal's work, and set the **background colour** and **colorMode** to HSB.

Before starting the actual work, I have organized the things that need to be coded using the **comment function** to ensure a smoother work environment.

As you can see in the image above, this work can be divided into three parts.
- Egg white part
- Egg yolk part
- The part that expresses the sparkle of egg yolk

_The egg yolk and the shiny part of the egg yolk can be added by creating a single image, but I wanted to use only P5.js as much as possible to utilize coding, so I divided it into different parts._

![reference1](/240310_second_HW/reference_wavy.png)
[Source: 5_2_5 Noise Circle
by eevirutanen](https://editor.p5js.org/eevirutanen/sketches/FuLEYWUu8)

I started with the egg white part first. In Rafaël Rozendaal's work, you can see the whites of eggs waving. To express this, I referred to the *"Noise Circle"* code created by eevirutanen.

![changed let setting](/240310_second_HW/change_let.png)

Referring to the *"Noise Circle"* code created by eevirutanen, I adjusted the **let** value to resemble Rafaël Rozendaal's egg white part.

![filling ellipse](/240310_second_HW/fill.png)

I added **noStroke** and **fill** to express egg whites.
_The background colour was temporarily changed to dark so that the egg whites can be easily seen._

![reference of shadow](/240310_second_HW/shadow.png)
[Source: Example of drawingContext](https://p5js.org/reference/#/p5/drawingContext)

Then, while looking for a way to apply a shadow to egg whites, I came across the **drawingContext** function.

![applied shadow](/240310_second_HW/apply_shadow.png)

Referring to the example code of the **drawingContext** function, I applied the shadow by adjusting the value according to the position of the egg white.

In this way, the first part of the work, egg white coding, was completed.

![yolk colour](/240310_second_HW/yolk_colour.png)

Secondly, I started making the second part of the piece, the egg yolk. First, to check the colours Rafaël Rozendaal used in his work, I used Adobe Photoshop's Color Picker to find the colour value of the egg yolk.

_At this time, I set the colorMode to HSB, so I used HSB values rather than RGB values._

![yolk shape](/240310_second_HW/yolk_shape.png)

The **fill** was set to the colour value of the egg yolk found using the Color Picker, and the shape and position of the egg yolk were set using the **ellipse function** and **translate function**.

![push and pop](/240310_second_HW/push_pop.png)
[Source: Description of push() and pop()](https://p5js.org/reference/#/p5/push)

However, during this process, a problem occurred where the egg yolk was not visible.

While looking for a way to solve this, I learned about **push** and **pop** functions.

![yolk appear](/240310_second_HW/yolk_appear.png)

When I applied these funtion to each part, even the egg yolk appeared successfully!!

![reference of the translate](/240310_second_HW/translate.png)
[Source: Example of translate](https://p5js.org/reference/#/p5/translate)

Additionally, if you look detailedly at Rafaël Rozendaal's work, you will see that egg yolks are also in motion.

While looking for a way to express this, I found a similar example on the P5 reference page.

![apply translate](/240310_second_HW/apply_trans.png)

By adjusting the value of the **translate** function by referring to the code in the example above, I was able to obtain egg yolk movement similar to Rafaël Rozendaal's work.

<<<<<<< HEAD
![first attemp to exprees shiny part of the egg yolk ](/240310_second_HW/square_shiny.png)

The final step is to express the third part of the work, the shiny part of the egg yolk.

To express this, I first used the **rect function** and **rotate function** to create a diagonally inclined rectangular shape.

However, if you look at Rafaël Rozendaal's work, you can see that the shiny part of the egg yolk is not a straight rectangle, but a natural curve along the round part of the egg yolk.

I thought it would be difficult to express this with just the rect function, so I decided to find another way.

=======
![first attempt to express the shiny part of egg yolk](/240310_second_HW/square_shiny.png)


>>>>>>> 49f3c48c0e85c67566715b30b4dfe28645ec0353
![how to make curve shape](/240310_second_HW/curve_shape.png)
[Source: Example of curveVertex()](https://p5js.org/reference/#/p5/curveVertex)

While looking for a way to create a curved shape for my second attempt at the shiny part of the egg yolk, I learned about the **curveVertex funtion**.

![made a shape of yolk shiny](/240310_second_HW/yolk_shiny.png)

To use the **curveVertex funtion**, I need to know the x and y coordinates of the shape. There is also a way to enter them one by one, but this takes a long time and it is difficult to predict the exact value.

Therefore, I used Adobe Illustrator's pen tool to create a shape similar to the shiny part of Rafaël Rozendaal's egg yolk and checked the x and y coordinate values of each anchor.

![located yolk shiny](/240310_second_HW/yolk_shiny_locate.png)

The x and y coordinate values confirmed through the above process were applied to the **curveVertex funtion**.

![fill the colour of yolk](/240310_second_HW/fill_yolk.png)

Lastly, I set the values of **fill funtion** and **noStroke funtion**, and applied the same **translate function** as the egg yolk so that the egg yolk and the shiny part of the egg yolk move together.

![final code](/240310_second_HW/final_code.png)

Ultimately, this is what the final code I wrote to replicate Rafaël Rozendaal's work looks like.
