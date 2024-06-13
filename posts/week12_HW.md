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

<img alt="Etch A Sketch" src="/240603_HW/Etch_A_Sketch.jpeg" width="100%">

_Source of [image](https://www.spinmaster.com/en-US/brands/etch-a-sketch/)_

The biggest design feature of Etch A Sketch is its flat gray screen with a red plastic frame. There are also two white handles on the bottom front corners of the frame. To express this, a shape was created.

```js
let num = 10000;
let range = 20;

let ax = [];
let ay = [];
let pointSizes = []; 

let isInitialized = false;
let direction = '';

function setup() {
  createCanvas(innerWidth, innerHeight);
  background('#970007');
  frameRate(30);
  
  noStroke();
  fill('#D90009');
  rect(5, 5, innerWidth - 10, innerHeight - 10, 10)

  stroke('#970007'); 
  fill(187); 
  let rectX = 30;
  let rectY = 108;
  let rectWidth = width - 60;
  let rectHeight = height - 200;
  let rectRadius = 20;
  strokeWeight(10); 
  rect(rectX, rectY, rectWidth, rectHeight, rectRadius);

  stroke('#970007');
  strokeWeight(5)
  
  // Dial
  stroke(187);
  fill('white');
  circle(45, height - 38, 50)
  circle(width - 40, height - 40, 50)

  
  // Drawing part
  for (let i = 0; i < num; i++) {
    pointSizes[i] = random(1, 10); 
    ax[i] = width / 2; 
    ay[i] = height / 2;
  }
}

function draw() {
  if (isInitialized) {
    for (let i = 1; i < num; i++) {
      ax[i - 1] = ax[i];
      ay[i - 1] = ay[i];
    }

    if (direction === 'left') {
      ax[num - 1] -= range;
    } else if (direction === 'right') {
      ax[num - 1] += range;
    } else if (direction === 'up') {
      ay[num - 1] -= range;
    } else if (direction === 'down') {
      ay[num - 1] += range;
    } else {
      ax[num - 1] += random(-range, range);
      ay[num - 1] += random(-range, range);
    }

    
    ax[num - 1] = constrain(ax[num - 1], 30 + 10, width - 30 - 10);
    ay[num - 1] = constrain(ay[num - 1], 108 + 10, height - 92 - 10);


    strokeWeight(2); 
    for (let j = 1; j < num; j++) {
      let val = j / num * 204.0 + 51;
      stroke(85);
      if (ax[j - 1] >= 40 && ax[j - 1] <= width - 40 &&
          ay[j - 1] >= 118 && ay[j - 1] <= height - 102 &&
          ax[j] >= 40 && ax[j] <= width - 40 &&
          ay[j] >= 118 && ay[j] <= height - 102) {
        line(ax[j - 1], ay[j - 1], ax[j], ay[j]);
      }
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
I then added text to convey the operation and planning intent. Although most letter keys have an added directional control, their function is to display the text as a picture as you write it. Therefore, 'J', 'I', 'K', and 'L', which typically serve as arrow keys, are displayed with arrows to express that you can draw not only randomly generated linear images, but also draw as you wish.

```js
let num = 10000;
let range = 20;

let ax = [];
let ay = [];
let pointSizes = []; 

let isInitialized = false;
let direction = '';
let font;

function preload() {
  font = loadFont('PixelifySans-VariableFont_wght.ttf');
}

function setup() {
  createCanvas(innerWidth, innerHeight);
  background('#970007');
  frameRate(30);
  
  noStroke();
  fill('#D90009');
  rect(5, 5, innerWidth - 10, innerHeight - 10, 10)


  stroke('#970007'); 
  fill(187); 
  let rectX = 30;
  let rectY = 108;
  let rectWidth = width - 60;
  let rectHeight = height - 200;
  let rectRadius = 20;
  strokeWeight(10); 
  rect(rectX, rectY, rectWidth, rectHeight, rectRadius);


  stroke('#970007');
  strokeWeight(5)
  
  fill('#FFEA75');
  textFont(font);
  textSize(90);
  text('Click', width / 2 - 113, 72);
  text('Click', width / 2 - 115, 70);
  textSize(20);
  text('to create a drawing!', width / 2 - 118, 91);
  text('to create a drawing!', width / 2 - 120, 90);
  
  // Dials
  stroke(187);
  fill('white');
  circle(45, height - 38, 50)
  circle(width - 40, height - 40, 50)
  
  // arrows
  noStroke();
  fill(255, 100);
  beginShape();
  vertex(20, height - 75);
  vertex(30, height - 82);
  vertex(30, height - 77);
  vertex(60, height - 77);
  vertex(60, height - 82);
  vertex(70, height - 75);
  vertex(60, height - 68);
  vertex(60, height - 72);
  vertex(30, height - 72);
  vertex(30, height - 68);
  endShape();
  
  beginShape();
  vertex(width - 79, height - 69);
  vertex(width - 72, height - 59);
  vertex(width - 76, height - 59);
  vertex(width - 76, height - 29);
  vertex(width - 72, height - 29);
  vertex(width - 79, height - 19);
  vertex(width - 86, height - 29);
  vertex(width - 82, height - 29);
  vertex(width - 82, height - 59);
  vertex(width - 86, height - 59);
  endShape();
  
  textSize(14);
  text('j', 10, height - 71);
  text('l', 73, height - 70);
  text('i', width - 81, height - 72);
  text('k', width - 83, height - 8);
  
  noStroke();
  fill(0, 50);
  textFont(font);
  textSize(19);
  text('If you write down the thoughts that come to your mind through the keyboard,', width / 2 - 348, height / 1.09);
  text('a picture will be drawn according to your thoughts.', width / 2 - 248, height / 1.05);
  
  fill(255, 130);
  text('If you write down the thoughts that come to your mind through the keyboard,', width / 2 - 350, height / 1.09);
  text('a picture will be drawn according to your thoughts.', width / 2 - 250, height / 1.05);

  
  
  // Drawing part
  for (let i = 0; i < num; i++) {
    pointSizes[i] = random(1, 10); 
    ax[i] = width / 2; 
    ay[i] = height / 2;
  }
}

function draw() {
  if (isInitialized) {
    for (let i = 1; i < num; i++) {
      ax[i - 1] = ax[i];
      ay[i - 1] = ay[i];
    }

    if (direction === 'left') {
      ax[num - 1] -= range;
    } else if (direction === 'right') {
      ax[num - 1] += range;
    } else if (direction === 'up') {
      ay[num - 1] -= range;
    } else if (direction === 'down') {
      ay[num - 1] += range;
    } else {
      ax[num - 1] += random(-range, range);
      ay[num - 1] += random(-range, range);
    }

    
    ax[num - 1] = constrain(ax[num - 1], 30 + 10, width - 30 - 10);
    ay[num - 1] = constrain(ay[num - 1], 108 + 10, height - 92 - 10);


    strokeWeight(2); 
    for (let j = 1; j < num; j++) {
      let val = j / num * 204.0 + 51;
      stroke(85);
      if (ax[j - 1] >= 40 && ax[j - 1] <= width - 40 &&
          ay[j - 1] >= 118 && ay[j - 1] <= height - 102 &&
          ax[j] >= 40 && ax[j] <= width - 40 &&
          ay[j] >= 118 && ay[j] <= height - 102) {
        line(ax[j - 1], ay[j - 1], ax[j], ay[j]);
      }
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

// keyboard function
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

But there's still the most important step left. This is the **real-time drawing** function. This is a very important function for expressing mycelial creativity. It expresses the core concepts of mycelial creativity: networks, connectivity, collaboration and interaction. The creative process enhanced by collaboration can be achieved with real-time drawing capabilities. By drawing and exchanging opinions on the same web page at the same time, ideas can be combined to produce more innovative results.

To implement this feature, I found a way to share the Drawing Canvas of p5.js, and was able to get it working through four **WebSockets and p5.js Tutorial** videos on [The Coding Train](https://www.youtube.com/watch?v=bjULmG8fqc8).

![Coding Train](/240603_HW/coding_train.png)

By watching the video, I understood the concept of real-time sharing and applied it to my code to make it work.

![shared drawing canvas](/240603_HW/play.png)
And finally, I have implemented the ability to draw pictures at the same time on one web page!!

# Final code
<iframe src="https://editor.p5js.org/s4002155/full/IrBmPhp3y" width="100%" height="810px"></iframe>

_It can run through the **http://localhost:3000** link, but there is a problem that you have to have the file on the computer to run it and run it through the terminal. The real-time drawing feature doesn't work, but I'll attach the p5.js file on the blog so you can experience the code._

### index.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/addons/p5.sound.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>
```
### server.js
```js
var express = require('express');

var app = express();
var server = app.listen(3000);

app.use(express.static('public'));

console.log("My socket server is running");

var socket = require('socket.io');

var io = socket(server);

io.on('connection', newConnection);

function newConnection(socket) {
    console.log('new connection: ' + socket.id);

    socket.on('line', lineMsg);

    function lineMsg(data) {
        socket.broadcast.emit('line', data);
        console.log(data);
    }
}
```
### sketch.js
```js
var socket;

let num = 10000;
let range = 20;

let ax = [];
let ay = [];
let pointSizes = []; 

let isInitialized = false;
let direction = '';
let font;

function preload() {
  font = loadFont('PixelifySans-VariableFont_wght.ttf');
}

function setup() {
  createCanvas(innerWidth, innerHeight);
  background('#970007');
  frameRate(30);

  socket = io.connect('http://localhost:3000')
  socket.on('line', newDrawing);
  
  noStroke();
  fill('#D90009');
  rect(5, 5, innerWidth - 10, innerHeight - 10, 10)


  stroke('#970007'); 
  fill(187); 
  let rectX = 30;
  let rectY = 108;
  let rectWidth = width - 60;
  let rectHeight = height - 200;
  let rectRadius = 20;
  strokeWeight(10); 
  rect(rectX, rectY, rectWidth, rectHeight, rectRadius);


  stroke('#970007');
  strokeWeight(5)
  
  fill('#FFEA75');
  textFont(font);
  textSize(90);
  text('Click', width / 2 - 113, 72);
  text('Click', width / 2 - 115, 70);
  textSize(20);
  text('to create a drawing!', width / 2 - 118, 91);
  text('to create a drawing!', width / 2 - 120, 90);
  
  // Dial
  stroke(187);
  fill('white');
  circle(45, height - 38, 50)
  circle(width - 40, height - 40, 50)
  
  //arrow
  noStroke();
  fill(255, 100);
  beginShape();
  vertex(20, height - 75);
  vertex(30, height - 82);
  vertex(30, height - 77);
  vertex(60, height - 77);
  vertex(60, height - 82);
  vertex(70, height - 75);
  vertex(60, height - 68);
  vertex(60, height - 72);
  vertex(30, height - 72);
  vertex(30, height - 68);
  endShape();
  
  beginShape();
  vertex(width - 79, height - 69);
  vertex(width - 72, height - 59);
  vertex(width - 76, height - 59);
  vertex(width - 76, height - 29);
  vertex(width - 72, height - 29);
  vertex(width - 79, height - 19);
  vertex(width - 86, height - 29);
  vertex(width - 82, height - 29);
  vertex(width - 82, height - 59);
  vertex(width - 86, height - 59);
  endShape();
  
  textSize(14);
  text('j', 10, height - 71);
  text('l', 73, height - 70);
  text('i', width - 81, height - 72);
  text('k', width - 83, height - 8);
  
  noStroke();
  fill(0, 50);
  textFont(font);
  textSize(19);
  text('If you write down the thoughts that come to your mind through the keyboard,', width / 2 - 348, height / 1.09);
  text('a picture will be drawn according to your thoughts.', width / 2 - 248, height / 1.05);
  
  fill(255, 130);
  text('If you write down the thoughts that come to your mind through the keyboard,', width / 2 - 350, height / 1.09);
  text('a picture will be drawn according to your thoughts.', width / 2 - 250, height / 1.05);


  // Drawing part
  for (let i = 0; i < num; i++) {
    pointSizes[i] = random(1, 10); 
    ax[i] = width / 2; 
    ay[i] = height / 2;
  }
}

function newDrawing(data) {
  let x1 = constrain(data.prevX, 40, width - 40);
  let y1 = constrain(data.prevY, 118, height - 102);
  let x2 = constrain(data.x, 40, width - 40);
  let y2 = constrain(data.y, 118, height - 102);

  strokeWeight(2);
  stroke('red');
  line(x1, y1, x2, y2);
}



function draw() {
  if (isInitialized) {
    for (let i = 1; i < num; i++) {
      ax[i - 1] = ax[i];
      ay[i - 1] = ay[i];
    }

    if (direction === 'left') {
      ax[num - 1] -= range;
    } else if (direction === 'right') {
      ax[num - 1] += range;
    } else if (direction === 'up') {
      ay[num - 1] -= range;
    } else if (direction === 'down') {
      ay[num - 1] += range;
    } else {
      ax[num - 1] += random(-range, range);
      ay[num - 1] += random(-range, range);
    }

    
    ax[num - 1] = constrain(ax[num - 1], 30 + 10, width - 30 - 10);
    ay[num - 1] = constrain(ay[num - 1], 108 + 10, height - 92 - 10);

    console.log(`Point ${num - 1}: (${ax[num - 1]}, ${ay[num - 1]})`);

    var data = {
      prevX: ax[num - 2], 
      prevY: ay[num - 2], 
      x: ax[num - 1],     
      y: ay[num - 1]      
    }
    socket.emit('line', data);

    strokeWeight(2); 
    for (let j = 1; j < num; j++) {
      let val = j / num * 204.0 + 51;
      stroke(85);
      if (ax[j - 1] >= 40 && ax[j - 1] <= width - 40 &&
          ay[j - 1] >= 118 && ay[j - 1] <= height - 102 &&
          ax[j] >= 40 && ax[j] <= width - 40 &&
          ay[j] >= 118 && ay[j] <= height - 102) {
        line(ax[j - 1], ay[j - 1], ax[j], ay[j]);
      }
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

# Video

