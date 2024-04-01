---
title: Response to other Rafaël Rozendaal's work
published_at: 2024-03-15
snippet: Second Homework for W2
disable_html_sanitization: true
---

<div align="center">
<iframe src="https://editor.p5js.org/s4002155/full/GOK_wIBRA" width="100%x" height="542px"></iframe>
</div>

_This is the end result, what I copied Rafaël Rozendaal's work as closely as possible._

# Which work by Rafaël Rozendaal did I choose?
![on an doff
by Rafaël Rozendaal](/240315_second_HW/onandoff.png)
[Source: on and off
by Rafaël Rozendaal](https://www.onandoff.org/)

Among Rafaël Rozendaal's various works, I chose **on and off .org**, created in 2003. The biggest feature of this work is that the switch icon changes depending on the mouse movement.

## working process
![created switch icons](/240315_second_HW/illust_icon.png)
This work is made up of switch icons. I could have created this icon through p5.js like the last respone, but the icon would be a bit complicated to implement with code, so I decided to use a method that loads the icon as an image to try a new method that is different from the last time.

Therefore, the first thing I did was create an on and off switch icon using Adobe Illustrator.

![setup background](/240315_second_HW/setup.png)
Next, in p5.js, the canvas size was set to **windowWidth** and **windowHeight** as in the original work, and the background color was set to white.

![loaded the On switch image](/240315_second_HW/loadImage_on.png)
Since I decided to work on this work by loading an image created as an illustration, I used the **function preload ()** code so that the switch icon created as an illustration could be uploaded.

![class On image](/240315_second_HW/class_on.png)

[Source: 8.4.1 Importing Image Assets - Frogger - p5.js Tutorial
by xin xin](https://www.youtube.com/watch?v=pbUyIhtGuhc)

The biggest feature of this operation is that the switch icon changes depending on the mouse movement. Therefore, I had to load the initial image at a certain location and code it so that the image changes when a specific action is performed. While thinking about how to do this, I figured out how to define a specific image using **class()** code. Since I grasped the concept of class() code through the first homework of week 2, I decided to use this method.

In this process, the 'class()' code was used to set the size and position of the switch image corresponding to on.

![loaded the Off switch image ](/240315_second_HW/loadImage_off.png)
Then, after confirming that the code worked well, I loaded the off switch image in the same way as the on switch.

![changeImage function](/240315_second_HW/changeImage.png)
Now it's time to code so that the switch image changes depending on the mouse movement. If you look at the original work, you can see that the image of the switch changes when the position of mouseY changes. In other words, when the mouse is placed on the switch button, the image changes to that image. To express this, I used the 'if () else ()' code to set the image to change depending on the position of mouseY.

![final code of on and off](/240315_second_HW/final_code.png)
This is what the final code looks like.

## Challenge
If you look closely at the original work, you can see that the image does not change simply by changing the position of mouseY, but rather changes depending on exactly when the mouse is on the switch button. I tried to implement this, but problems arose where it did not work properly, perhaps because the code required too many things at once. (I tried fixing the position of mouseX.)

Therefore, although I could not perfectly follow the original work, I tried to implement it similarly through the position of mouseY.