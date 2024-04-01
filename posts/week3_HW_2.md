---
title: AT1 Journeys
published_at: 2024-03-21
snippet: Second Homework for W3
disable_html_sanitization: true
---

# Choose another work by Rafaël Rozendaal that I will be responding to with your AT1 submission.
<div align="center">
<iframe src="https://www.lookingatsomething.com/" width="100%" height="100%"></iframe>
</div>

[Source: looking at something
by Rafaël Rozendaal](https://www.lookingatsomething.com/)

I chose **looking at something .com**, created in 2013. The biggest feature of this work is that the weather changes depending on the movement of the mouse.

## What about the work makes it belong to the aesthetic category of "cute"?
In the aesthetic category, “cute” is intimate and domestic. This creates a desire for intimacy and is non-threatening. From this perspective, this work falls into the aesthetic category of “cute.”

Weather is one of the most intimate factors in our lives that affects us. The biggest feature of this work is the weather that changes depending on the position of the mouse, creating a rainy scene. Rafaël Rozendaal expressed rain through the repetition of small and simple shapes, which is one of the points that penetrates the concept of “cute” in the aesthetic category. Rain is formally simple, a small element and poses no threat to us.

## How does the artist employ effective complexity in the work to achieve its aesthetic result?
Applying the concept of “effective complexity” within a cute aesthetic frame allows you to combine seemingly simple elements to create emotional resonance. In this respect, Rafaël Rozendaal used a combination of simple elements. Despite their individual simplicity, such as the repeating rain forms and backgrounds rendered only in color without unnecessary graphics, he used these elements together to create compositions that were greater than the sum of their parts. Additionally, the concept of effective complexity emphasizes the balance between order and randomness within a cute aesthetic frame. Although repeating rain formations may appear orderly and harmonious, the rain is generated randomly. This balance between order and randomness enhances the overall complexity of the cute aesthetic, making it visually appealing and emotionally resonant.


# Document your creative process in responding to Rozendaal's work.

## What attributes of the original work would you like to retain? What aspects would you like to improve / change?
In fact, the original work falls short in many aspects to be included in the aesthetic category of “cute.” That's why I'd like to improve the original work to fit it more into the aesthetic category of "cute." I will make improvements in the ways by using the characteristics sucg as small, round shapes, soft colors. The original work, however, makes good use of “effective complexity” within a cute aesthetic framework. I want to maintain the attributes of the original work that balance between order and randomness by repeating seemingly simple visual elements. Additionally, the combination of visually simple elements, despite their individual simplicity, creates a composition that when brought together is greater than the sum of its parts. The arrangement and interaction of these elements contributes to the overall complexity of "cute," so I'd like to keep this part as well.

## In what way is your work in dialogue with the Rozendaal piece you have chosen?
The original piece, created by Rafaël Rozendaal, is designed as a scene viewed from the inside out. _(Like looking at the weather outside the window at home!)_ I tried to change perspective to communicate with Rafaël Rozendaal's work. The work will be structured as a design that looks from the outside in, rather than a scene looking out from the inside.

When considering how to express this, I also considered the aesthetic category of “cute.” When I thought of an object that could express "cute" while also having the characteristic of looking from the outside in, *"snowglobe"* came to mind. The snowglobe is a design that allows you to see the world inside the glass from outside the glass. Additionally, like the rain in Rafaël Rozendaal's original work, the snowglobe constitutes a snowy environment.

**Therefore, in my work, I will represent the snowglobe, providing a different perspective from Rafaël Rozendaal's work, but in a similar way, communicating with the original work.**

## Document and discuss how the javascript techniques and design concepts you are using contribute to the aesthetic register of your response.

![created background image](/240321_second_HW/illust_bg.png)
First of all, the biggest feature of the original work is that the weather changes depending on the position of mouseY. Rafaël Rozendaal expressed this through falling rain and a changing background. I also created a background using Adobe Illustrator to express the changing background.

The most important theme of this work is that it should fall under “cute” in the aesthetic category. To express this, I decided to create a cute, simple graphic in the background image. Also, because I had to indicate that it was a snowglobe, I designed it around a cute, round, small snowman.

<p align="center">
  <img alt="background1" src="/240321_second_HW/background1.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="background2" src="/240321_second_HW/background2.png "background2" width="45%">
</p>

These two images are background images I created. I wanted to express the movement of mouseY as 'shaking the snowglobe'. Therefore, the image on the left represents when the mouseY position is at the top of the canvas, that is, before shaking the snowglobe. The image on the right is what the snowglobe looks like after shaking it, so I added the appearance of piled snow and changed the background color because I wanted it to have more contrast. (when the mouseY position is at the bottom of the canvas)

![function setup](/240321_second_HW/setup.png)
After creating the background image, I started coding in earnest. To create a fullscreen work, I set the canvas size to **windoeWidth** and **windowHeight**.

![upload background images](/240321_second_HW/load_image.png)
Then, the file created as the background images was loaded through the 'funtion preload()' code.

_* At this time, this code is only a code to load the image and not an execution code, so it is not displayed on the screen._

![](/240321_second_HW/class.png)
The background was replaced with a created image, and the rain, which was the biggest feature of the original work, was decided to be improved to **snow**, which is the biggest characteristic of a snowglobe and is small and round in shape, which also falls under the aesthetic category of "cute."

[Source: Snowflakes
by Aatish Bhatia](https://p5js.org/examples/simulate-snowflakes.html)

While looking for a reference to express this, I found the "Snowflakes" example in p5.js. However, rather than using this code as is, I tried to apply the codes I had learned as much as possible. So, referring to this example, I first wrote the 'class ()' code that defines snowflake based on the code used in Rafaël Rozendaal's previous work.

![](/240321_second_HW/for_loop.png)
Additionally, the original work was designed so that it not only rains when the mouseY position moves from the top to the bottom of the canvas, but also disappears when the position of mouseY moves from the bottom to the top again. I used **iteration** and **boolean logic** to express this. When the position of mouseY moves from the top to the bottom, snowflakes are repeatedly produced. When the position of mouseY moves from the bottom to the top, snowflakes are not created, and at the same time, opacity is used to make existing snowflakes disappear.

![](/240321_second_HW/strange_snowflake.png)
This is what it looks like when the code written up to this point is executed.

![](/240321_second_HW/fill.png)
The snowflakes had outlines and were not colored so they did not look like snow. To solve this, I added the 'fill ()' code and 'noStroke ()' code to 'funtion setup ()' and changed it to look like a snowflake.

_*Because the snow is white, it was hard to see with the existing background color, so I temporarily changed the background to black._

![](/240321_second_HW/alpha_image.png)
After confirming that the snowflake was working properly, I wrote code to change the background depending on the position of mouseY, which is the second most important part of the work.

At this time, I needed the two background images to change naturally depending on the position of mouseY, so I placed the two background images overlapping and adjusted the **alpha** value to make it look like the images were changing depending on the position of mouseY.

![](/240321_second_HW/finale_code1.png)
![](/240321_second_HW/final_code2.png)
This is my final code.

<p align="center">
  <img alt="1" src="/240321_second_HW/1.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="2" src="/240321_second_HW/2.png "2" width="45%">
</p>
<p align="center">
  <img alt="3" src="/240321_second_HW/3.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="4" src="/240321_second_HW/4.png "4" width="45%">
</p>
If you run the code, you can see that it changes depending on the position of mouseY.

### Final result
<div align="center">
<iframe src="https://editor.p5js.org/s4002155/full/BBVE2j8Il" width="100%" height="542px"></iframe>
</div>

[Fullscreen version of my work](https://editor.p5js.org/s4002155/full/BBVE2j8Il)