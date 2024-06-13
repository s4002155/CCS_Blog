---
title: Documentation and discussion relating to my creative process for AT3
published_at: 2024-06-03
snippet: Week12 Homework
disable_html_sanitization: true
---
# Information / explanations to consider when assessing my AT3
The community I belong to is made up of people who love to draw, and I want to solve the problem of creative expression and idea depletion. For creative and unconventional new ideas, sometimes unimaginable ideas are a good source of inspiration. Therefore, I suggest a way to gain inspiration through randomly generated lines or shapes (or compositions) formed through lines. I also aim to promote collaboration and support through a real-time drawing feature that allows multiple users (community members) to draw on the same page at the same time. This allows community members to get on the same page at the same time, exchange ideas, be inspired by each other's work, and grow. You can also receive positive stimulation from seeing different drawing styles develop.

# Process
First of all, I wanted to write code that could draw like a whiteboard, so I decided to use **p5.js**, which is designed around graphics and visual expressions so that drawings, animations, graphic interactions, etc. can be easily implemented.

The biggest features of the project I will be creating are the randomly generated lines and the real-time drawing function. To implement this, I decided to first write code for **randomly generated lines**.

![reference code](/240603_HW/Brownian_Motion.png)
Referenced from [p5.js Examples](https://p5js.org/examples/simulate-brownian-motion.html)

To create randomly generated lines in p5.js, I referred to the example called "Brownian Motion". In this code, a random line trajectory is created through randomly generated points, and the points connected by lines are drawn on the screen to visualize the moving trajectory. This example was a code that effectively aligned with my goal of being inspired by shapes created through randomly generated lines. So I decided to develop this code.

```js
let num = 2000;
let range = 6;

let ax = [];
let ay = [];


function setup() {
  createCanvas(710, 400);
  for ( let i = 0; i < num; i++ ) {
    ax[i] = width / 2;
    ay[i] = height / 2;
  }
  frameRate(30);
}

function draw() {
  background(51);

  // Shift all elements 1 place to the left
  for ( let i = 1; i < num; i++ ) {
    ax[i - 1] = ax[i];
    ay[i - 1] = ay[i];
  }

  // Put a new value at the end of the array
  ax[num - 1] += random(-range, range);
  ay[num - 1] += random(-range, range);

  // Constrain all points to the screen
  ax[num - 1] = constrain(ax[num - 1], 0, width);
  ay[num - 1] = constrain(ay[num - 1], 0, height);

  // Draw a line connecting the points
  for ( let j = 1; j < num; j++ ) {
    let val = j / num * 204.0 + 51;
    stroke(val);
    line(ax[j - 1], ay[j - 1], ax[j], ay[j]);
  }
}
```
This is the original code that became my starting point. I wanted to modify (or add) two features to the existing code.
1. Instead of setting the starting position of the point to the center of the canvas, set the point clicked with the mouse as the starting position of the point.

2. Change the position of the dot using the keyboard. In other words, when the keyboard is not pressed, a random trajectory is drawn like the existing code, but when the keyboard is pressed, the point is set to move according to the keyboard value from the last point before the keyboard was pressed.

```js
let num = 2000;
let range = 6;

let ax = [];
let ay = [];
let isInitialized = false;

function setup() {
  createCanvas(710, 400);
  frameRate(30);
}

function draw() {
  background(51);

  if (isInitialized) {
    for (let i = 1; i < num; i++) {
      ax[i - 1] = ax[i];
      ay[i - 1] = ay[i];
    }

    ax[num - 1] += random(-range, range);
    ay[num - 1] += random(-range, range);

    ax[num - 1] = constrain(ax[num - 1], 0, width);
    ay[num - 1] = constrain(ay[num - 1], 0, height);

    for (let j = 1; j < num; j++) {
      let val = j / num * 204.0 + 51;
      stroke(val);
      line(ax[j - 1], ay[j - 1], ax[j], ay[j]);
    }
  }
}

function mousePressed() {
  for (let i = 0; i < num; i++) {
    ax[i] = mouseX;
    ay[i] = mouseY;
  }
  isInitialized = true;
}
```
I added the ```function mousePressed()``` so that a dot can be created when the mouse is clicked.

Next, I wanted to be able to adjust the direction of the line using the keyboard keys so that I could adjust the direction I wanted even among the randomly generated lines. While looking for materials to implement this, I found an example called ["Snake game"](https://p5js.org/examples/interaction-snake-game.html) that showed how to control direction through the keyboard. This code uses the 'J', 'I', 'K', and 'L' keys as arrow keys.

At this time, an idea occurred to me to further utilize the keyboard keys. The idea is to add direction control functions to more keys in addition to the 'J', 'I', 'K', and 'L' keys so that when you write down your diary or thoughts on the keyboard, you can draw a picture of them. Through this method, the picture does not have a fixed form, but continuously evolves and changes depending on the user's participation and changes. This is similar to the way mycelial adapt to environmental changes, and was consistent with the process of constant growth and transformation of the mycelial network, allowing for the expression of mycelial creativity. That's why I checked the [key code](https://www.toptal.com/developers/keycode) for each keyboard character and added direction control functions to various character keys.

```js
function keyPressed() {
  switch (keyCode) {
    case 65: // 'A' key
    case 74: // 'J' key
    case 81: // 'Q' key
    case 90: // 'Z' key
    case 97: // 'a' key
    case 106: // 'j' key
    case 113: // 'q' key
    case 122: // 'z' key
      if (direction !== 'right') {
        direction = 'left';
      }
      break;
    case 68: // 'D' key
    case 76: // 'L' key
    case 69: // 'E' key
    case 88: // 'X' key
    case 100: // 'd' key
    case 108: // 'l' key
    case 101: // 'e' key
    case 120: // 'x' key
      if (direction !== 'left') {
        direction = 'right';
      }
      break;
    case 87: // 'W' key
    case 73: // 'I' key
    case 82: // 'R' key
    case 89: // 'Y' key
    case 119: // 'w' key
    case 105: // 'i' key
    case 114: // 'r' key
    case 121: // 'y' key
      if (direction !== 'down') {
        direction = 'up';
      }
      break;
    case 83: // 'S' key
    case 75: // 'K' key
    case 70: // 'F' key
    case 86: // 'V' key
    case 115: // 's' key
    case 107: // 'k' key
    case 102: // 'f' key
    case 118: // 'v' key
      if (direction !== 'up') {
        direction = 'down';
      }
      break;
  }
}

function keyReleased() {
  direction = '';
}
```

When I modified the code in this way and ran the code, it looked just like "Etch A Sketch". Etch A Sketch is a drawing toy that allows you to create linear images with controls that allow you to move horizontally and vertically, and then use them to draw images. I felt that it was similar in that it was a  linear image, that it could be moved horizontally and vertically through the keyboard, and above all, that it could be drawn, so I decided to use Etch A Sketch as my design concept.

![Etch A Sketch](/240603_HW/Etch_A_Sketch.jpeg)
Source of [image](https://www.spinmaster.com/en-US/brands/etch-a-sketch/)





# Final code


# Video

