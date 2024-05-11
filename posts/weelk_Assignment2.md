---
title: Assignment2
published_at: 2024-05-04
snippet: About Assignment2 process and work
disable_html_sanitization: true
---
## Preview of finished work
<div align="center">
<iframe src="https://s4002155-ccs-assignm-85.deno.dev/" width="800px" height="500px"></iframe>
</div>

*_Move your mouse over the artwork and click!_

## Which artist's works did I respond to?
<p align="center">
  <img alt="Mathieu St-Pierre" src="/240504_Assignment2/Mathieu.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Kerry Mitchell" src="/240504_Assignment2/NATO.png "background2" width="45%">
</p>

<div>
Left image: 

[untitled by Mathieu St-Pierre](https://matstpierre.wordpress.com/2017/08/13/untitled-2/)
</div>

<div>
Right image:

[NATO by Kerry Mitchell](https://www.kerrymitchellart.com/gallery36/nato.html)
</div>

To achieve a zany and chaotic aesthetic, I decided to respond to the work of two artists. The first artist is glitch artist Mathieu St-Pierre. Glitch can be said to be the most representative chaotic aesthetic in the digital environment. That's why I thought it would be effective to respond to the work of glitch artist Mathieu St-Pierre to achieve a zany and chaotic aesthetic.

The second artist is fractal artist Kerry Mitchell. Fractals, created by repeating a simple process over and over again in a continuous feedback loop, are also effective in expressing a zany and chaotic aesthetic. I also thought that implementing complex patterns through text could add to the confusion if combined with graphics. For this reason I would like to respond to the work of these two artists.

## Process
_index.html_
```html
<!doctype html>
<head>
    <title> b l a n k </title>
</head>

<body>
   <canvas id="cnv_element"></canvas>
   <script src="script.js"></script>
</body>
```
_script.js_
```js
document.body.style.margin   = 0
document.body.style.overflow = `hidden`

const cnv = document.getElementById (`cnv_element`)
cnv.width = innerWidth
cnv.height = innerHeight

const ctx = cnv.getContext (`2d`)

const draw_frame = () => {
   ctx.fillStyle = `turquoise`
   ctx.fillRect (0, 0, innerWidth, innerHeight)

   requestAnimationFrame (draw_frame)
}

draw_frame ()

window.onresize = () => {
   cnv.width = innerWidth
   cnv.height = innerHeight   
}
```
Before I explain the process, I used [this template](https://github.com/capogreco/blank_net_art/tree/main/public) to create the net art. This template consists of **index.html** and **script.js**.

```js
document.body.style.margin = 0;
document.body.style.overflow = 'hidden';

const firstCanvas = document.getElementById("firstCanvas");
const renderer = new c2.Renderer(firstCanvas);

resize();

renderer.background('#000000');
```
First, I started by setting up the canvas. I slightly modified the existing template.

```js
    // First canvas code
document.body.style.margin = 0;
document.body.style.overflow = 'hidden';

const firstCanvas = document.getElementById("firstCanvas");
const renderer = new c2.Renderer(firstCanvas);

resize();

renderer.background('#000000');
let random = new c2.Random();

const maxWidth = 400; // Maximum width
const maxHeight = 200; // Maximum height    

class Agent extends c2.Cell {
    constructor(x, y) {
        let r = random.next(renderer.width / 40, renderer.width / 15);
        super(x, y, r);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
        // Select random color in neon or fluorescent
        this.color = randomNeonColor();
        // Generate random width and height
        this.randomWidth = Math.random() * maxWidth; // maxWidth is desired maximum width
        this.randomHeight = Math.random() * maxHeight; // maxHeight is desired maximum height
    }

    update() {
        this.p.x += this.vx;
        this.p.y += this.vy;

        if (this.p.x < 0) {
            this.p.x = 0;
            this.vx *= -1;
        } else if (this.p.x > renderer.width) {
            this.p.x = renderer.width;
            this.vx *= -1;
        }
        if (this.p.y < 0) {
            this.p.y = 0;
            this.vy *= -1;
        } else if (this.p.y > renderer.height) {
            this.p.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        if (this.state != 2) {
            renderer.stroke(c2.Color.rgb(50, .2));
            renderer.lineWidth(2);
            renderer.fill(this.color);
            renderer.rect(this.p.x, this.p.y, this.randomWidth, this.randomHeight); // Draw rectangle with random width and height
        }
    }
}

// Function to generate neon or fluorescent colors
function randomNeonColor() {
    let neonColors = ['#ff00ff', '#00ffff', '#ffaa00', '#00ff00', '#ff00aa', '#ffff00', '#00ffaa', '#ffaa00', '#00aaff', '#aa00ff'];
    return neonColors[Math.floor(Math.random() * neonColors.length)];
}

let agents = [];

// Generate agents
for (let i = 0; i < 15; i++) {
    let x = random.next(renderer.width);
    let y = random.next(renderer.height);
    agents.push(new Agent(x, y));
}

let lastMouseMoveTime = 0;
const minMouseMoveInterval = 100; // milliseconds

// Define the draw function of the renderer
renderer.draw(() => {
    let voronoi = new c2.LimitedVoronoi();
    voronoi.compute(agents);

    // Display and update agents
    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});

// Register window resize event handler
window.addEventListener('resize', resize);
// Register mouse move event handler
window.addEventListener('mousemove', onMouseMove);

// Window resize function
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}

// Mouse move event function
function onMouseMove(event) {
    let currentTime = Date.now();
    if (currentTime - lastMouseMoveTime > minMouseMoveInterval) {
        let x = event.clientX;
        let y = event.clientY;
        agents.push(new Agent(x, y));
        lastMouseMoveTime = currentTime;
    }
}
```
_* To add to the confusion, I referred to the [c2.js example](https://c2js.org/examples.html?name=LimitedVoronoi4). This example continues to create rectangles. By using this, it looks like an error window that is constantly created due to errors in a digital environment!!_

As I was thinking about a way to respond to glitch artwork while expressing its zany and chaotic aesthetic, I decided to take advantage of glitch's morphological characteristics. A glitch is when the pixels in a graphic appear momentarily different. This causes pixel-by-pixel garbled graphics to appear as if they are made up of squares of various sizes. To represent this, I decided to frame the artwork through squares of different sizes.

```js
let random = new c2.Random();

const maxWidth = 400; // Maximum width
const maxHeight = 200; // Maximum height    

class Agent extends c2.Cell {
    constructor(x, y) {
        let r = random.next(renderer.width / 40, renderer.width / 15);
        super(x, y, r);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
        // Select random color in neon or fluorescent
        this.color = randomNeonColor();
        // Generate random width and height
        this.randomWidth = Math.random() * maxWidth; // maxWidth is desired maximum width
        this.randomHeight = Math.random() * maxHeight; // maxHeight is desired maximum height
    }

    update() {
        this.p.x += this.vx;
        this.p.y += this.vy;

        if (this.p.x < 0) {
            this.p.x = 0;
            this.vx *= -1;
        } else if (this.p.x > renderer.width) {
            this.p.x = renderer.width;
            this.vx *= -1;
        }
        if (this.p.y < 0) {
            this.p.y = 0;
            this.vy *= -1;
        } else if (this.p.y > renderer.height) {
            this.p.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        if (this.state != 2) {
            renderer.stroke(c2.Color.rgb(50, .2));
            renderer.lineWidth(2);
            renderer.fill(this.color);
            renderer.rect(this.p.x, this.p.y, this.randomWidth, this.randomHeight); // Draw rectangle with random width and height
        }
    }
}

let agents = [];

// Generate agents
for (let i = 0; i < 15; i++) {
    let x = random.next(renderer.width);
    let y = random.next(renderer.height);
    agents.push(new Agent(x, y));

// Define the draw function of the renderer
renderer.draw(() => {
    let voronoi = new c2.LimitedVoronoi();
    voronoi.compute(agents);

    // Display and update agents
    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});
```
To do this, I wrote code to draw randomly moving rectangular agents using ```class {}``` code. Rectangles are generated randomly from among the 'maximum width' and 'maximum height' values, so the generated rectangles are random and can be confusing. Also, through the ```update()``` code, I set the rectangle to move in the opposite direction when it goes beyond the boundaries of the canvas. 'agents', an array containing agents, creates agents at random locations and adds them to the array.

```js
// Function to generate neon or fluorescent colors
function randomNeonColor() {
    let neonColors = ['#ff00ff', '#00ffff', '#ffaa00', '#00ff00', '#ff00aa', '#ffff00', '#00ffaa', '#ffaa00', '#00aaff', '#aa00ff'];
    return neonColors[Math.floor(Math.random() * neonColors.length)];
}
```
Additionally, to enhance the characteristics of the glitch, the colour of the square is displayed in a neon or fluorescent colour that matches the glitch theme.

```js
let lastMouseMoveTime = 0;
const minMouseMoveInterval = 100; // milliseconds

// Register mouse move event handler
window.addEventListener('mousemove', onMouseMove);

// Mouse move event function
function onMouseMove(event) {
    let currentTime = Date.now();
    if (currentTime - lastMouseMoveTime > minMouseMoveInterval) {
        let x = event.clientX;
        let y = event.clientY;
        agents.push(new Agent(x, y));
        lastMouseMoveTime = currentTime;
    }
}
```
To further add to the confusion, I added a move event. Through this move event, more rectangles are randomly created each time the mouse is moved.


```js
// Second canvas code
// TAU is nicer than PI for trig
const TAU = Math.PI * 2;

// get canvas element & assign to 'cnv'
const secondCanvas = document.getElementById("secondCanvas");

// Define function for resizing canvas
function resize_canvas() {
    // Resize canvas to = viewport
    secondCanvas.width = innerWidth;
    secondCanvas.height = innerHeight;
}

// Assign to .onresize property of window
window.onresize = resize_canvas;

// Initialise canvas size
resize_canvas();

// Get canvas context & assign to 'ctx'
const ctx2 = secondCanvas.getContext('2d');

// Empty array for square objects to go in
const squuares = [];

// Assign to 'mouse_pos' a newly instantiated vector
const mouse_pos = new Vector(0, 0);

// Load ASCII art from file
let ascii_art;
fetch('ascii_art.txt')
    .then(response => response.text())
    .then(data => {
        ascii_art = data;
        // Split ASCII art into lines
        const lines = ascii_art.split('\n');
        // Draw ASCII art on canvas
        ctx2.fillStyle = 'black';
        ctx2.font = '6px monospace'; // Adjust font size here
        ctx2.textAlign = 'left';
        ctx2.textBaseline = 'top';
        // Draw each line of ASCII art
        lines.forEach((line, index) => {
            ctx2.fillText(line, 0, index * 6); // Adjust font size here
        });
        // Kick off the recursive animation sequence
        requestAnimationFrame(draw_frame);
    })
    .catch(error => console.error('Error loading ASCII art:', error));

// Whenever the pointer moves
secondCanvas.onpointermove = pointer_event => {
    // Update the x & y properties of 'mouse_pos' to
    // reflect the x & y properties of the pointer
    mouse_pos.x = pointer_event.x;
    mouse_pos.y = pointer_event.y;
};

// Whenever there is a touch or mouse click
secondCanvas.onpointerdown = pointer_event => {
    // Add an object to the squuares array, in which
    squuares.push({
        // The position = the x & y coordinates of the pointer
        p: new Vector(pointer_event.x, pointer_event.y),
        // The velocity = random direction w magnitude of 18
        v: vector_from_angle(Math.random() * TAU, 18)
    });
};

// Define the recursive animation sequence
function draw_frame() {
    // Clear canvas
    ctx2.clearRect(0, 0, secondCanvas.width, secondCanvas.height);

    // For each square in the 'squuares' array
    squuares.forEach(s => {
        // Random angle for nudge
        const nudge_angle = Math.random() * TAU;

        // Random magnitude for nudge
        const nudge_mag = Math.random() * 8;

        // Create nudge vector
        const nudge = vector_from_angle(nudge_angle, nudge_mag);

        // Nudge the square's position
        s.p.add(nudge);

        // Acceleration: start with a clone of 'mouse_pos'
        const acc = mouse_pos.clone();

        // Subtract the position of the square
        acc.subtract(s.p);

        // Set magnitude to 1
        acc.set_mag(1);

        // Add acceleration to the square's velocity
        s.v.add(acc);

        // If square's velocity is > 18, reduce to 18
        if (s.v.mag() > 18) s.v.set_mag(18);

        // Add velocity to the square's position
        s.p.add(s.v);

        // Draw the ASCII art at the position
        ctx2.fillStyle = 'white';
        ctx2.font = '6px monospace'; // Adjust font size here
        // Draw each line of ASCII art
        const lines = ascii_art.split('\n');
        lines.forEach((line, index) => {
            ctx2.fillText(line, s.p.x, s.p.y + (index * 6)); // Adjust font size here
        });
    });

    // Call the next frame
    requestAnimationFrame(draw_frame);
}
```
_* To add more zany and chaotic aesthetic, I referred to the [Pointer Interaction example](https://github.com/capogreco/interaction_example). In this example, the rectangle created moves chaotically with each mouse click. Not only can I get more confusing results, but I can also add zany elements through the graphics generated when you click the mouse._

```js
class Vector {
   constructor (x, y) {
      this.x = x
      this.y = y
   }

   add (v) {
      this.x += v.x
      this.y += v.y
   }

   subtract (v) {
      this.x -= v.x
      this.y -= v.y
   }

   mult (m) {
      this.x *= m
      this.y *= m
   }

   mag () { 
      // using a^2 + b^2 = c^2
      return ((this.x ** 2) + (this.y ** 2)) ** 0.5
   }

   set_mag (m) {
      const safe_mag = this.mag ()
      if (safe_mag == 0) return
      this.mult (m / safe_mag)
   }

   rotate (a) {
      // https://matthew-brett.github.io/teaching/rotation_2d.html

      const new_x = (this.x * Math.cos (a)) - (this.y * Math.sin (a))
      const new_y = (this.x * Math.sin (a)) + (this.y * Math.cos (a))

      this.x = new_x
      this.y = new_y
   }

   clone () {
      return new Vector (this.x, this.y)
   }
}

function vector_from_angle (angle, magnitude) {
   const x = magnitude * Math.cos (angle)
   const y = magnitude * Math.sin (angle)
   return new Vector (x, y)
}
```
First of all, to refer to this example, a vector must be defined using class code, so 'vector.js' was used.

```js
// Second canvas code
// TAU is nicer than PI for trig
const TAU = Math.PI * 2;

// get canvas element & assign to 'cnv'
const secondCanvas = document.getElementById("secondCanvas");

// Define function for resizing canvas
function resize_canvas() {
    // Resize canvas to = viewport
    secondCanvas.width = innerWidth;
    secondCanvas.height = innerHeight;
}

// Assign to .onresize property of window
window.onresize = resize_canvas;

// Initialise canvas size
resize_canvas();

// Get canvas context & assign to 'ctx'
const ctx2 = secondCanvas.getContext('2d');
```
I wanted to apply this example on top of the artwork I created by referring to the c2.js example, so I created two separate canvases, and placed the second canvas on top of the first canvas to create a layer effect.


<p align="center">
  <img alt="created 404 icon" src="/240504_Assignment2/create.png" width="48%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="generate image to ascii" src="/240504_Assignment2/ascii.png "background2" width="45%">
</p>

In the existing code, a square appeared when you clicked the mouse, but to add to the aesthetic of zany and chaotic, I decided to display a '404' icon, which represents an error different from a 'glitch' in a digital environment. Additionally, to reflect the idea of creating confusion through text in fractal artwork, I tried ASCII art by converting the image to ASCII characters via [this link](https://asciiart.club/).

![ASCII code](/2240504_Assignment2/asciicode.png)

The icon converted to ASCII characters looks like this.

```js
// Assign to 'mouse_pos' a newly instantiated vector
const mouse_pos = new Vector(0, 0);

// Load ASCII art from file
let ascii_art;
fetch('ascii_art.txt')
    .then(response => response.text())
    .then(data => {
        ascii_art = data;
        // Split ASCII art into lines
        const lines = ascii_art.split('\n');
        // Draw ASCII art on canvas
        ctx2.fillStyle = 'black';
        ctx2.font = '6px monospace'; // Adjust font size here
        ctx2.textAlign = 'left';
        ctx2.textBaseline = 'top';
        // Draw each line of ASCII art
        lines.forEach((line, index) => {
            ctx2.fillText(line, 0, index * 6); // Adjust font size here
        });
        // Kick off the recursive animation sequence
        requestAnimationFrame(draw_frame);
    })
    .catch(error => console.error('Error loading ASCII art:', error));

// Whenever the pointer moves
secondCanvas.onpointermove = pointer_event => {
    // Update the x & y properties of 'mouse_pos' to
    // reflect the x & y properties of the pointer
    mouse_pos.x = pointer_event.x;
    mouse_pos.y = pointer_event.y;
};

// Whenever there is a touch or mouse click
secondCanvas.onpointerdown = pointer_event => {
    // Add an object to the squuares array, in which
    squuares.push({
        // The position = the x & y coordinates of the pointer
        p: new Vector(pointer_event.x, pointer_event.y),
        // The velocity = random direction w magnitude of 18
        v: vector_from_angle(Math.random() * TAU, 18)
    });
};

// Define the recursive animation sequence
function draw_frame() {
    // Clear canvas
    ctx2.clearRect(0, 0, secondCanvas.width, secondCanvas.height);

    // For each square in the 'squuares' array
    squuares.forEach(s => {
        // Random angle for nudge
        const nudge_angle = Math.random() * TAU;

        // Random magnitude for nudge
        const nudge_mag = Math.random() * 8;

        // Create nudge vector
        const nudge = vector_from_angle(nudge_angle, nudge_mag);

        // Nudge the square's position
        s.p.add(nudge);

        // Acceleration: start with a clone of 'mouse_pos'
        const acc = mouse_pos.clone();

        // Subtract the position of the square
        acc.subtract(s.p);

        // Set magnitude to 1
        acc.set_mag(1);

        // Add acceleration to the square's velocity
        s.v.add(acc);

        // If square's velocity is > 18, reduce to 18
        if (s.v.mag() > 18) s.v.set_mag(18);

        // Add velocity to the square's position
        s.p.add(s.v);

        // Draw the ASCII art at the position
        ctx2.fillStyle = 'white';
        ctx2.font = '6px monospace'; // Adjust font size here
        // Draw each line of ASCII art
        const lines = ascii_art.split('\n');
        lines.forEach((line, index) => {
            ctx2.fillText(line, s.p.x, s.p.y + (index * 6)); // Adjust font size here
        });
    });

    // Call the next frame
    requestAnimationFrame(draw_frame);
}
```
Then, using the code referenced in the example, when you click the mouse, a 404 icon converted to ASCII art appears and moves confusingly depending on the mouse movement.

# Final code
```js
    // First canvas code
document.body.style.margin = 0;
document.body.style.overflow = 'hidden';

const firstCanvas = document.getElementById("firstCanvas");
const renderer = new c2.Renderer(firstCanvas);

resize();

renderer.background('#000000');
let random = new c2.Random();

const maxWidth = 400; // Maximum width
const maxHeight = 200; // Maximum height    

class Agent extends c2.Cell {
    constructor(x, y) {
        let r = random.next(renderer.width / 40, renderer.width / 15);
        super(x, y, r);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
        // Select random color in neon or fluorescent
        this.color = randomNeonColor();
        // Generate random width and height
        this.randomWidth = Math.random() * maxWidth; // maxWidth is desired maximum width
        this.randomHeight = Math.random() * maxHeight; // maxHeight is desired maximum height
    }

    update() {
        this.p.x += this.vx;
        this.p.y += this.vy;

        if (this.p.x < 0) {
            this.p.x = 0;
            this.vx *= -1;
        } else if (this.p.x > renderer.width) {
            this.p.x = renderer.width;
            this.vx *= -1;
        }
        if (this.p.y < 0) {
            this.p.y = 0;
            this.vy *= -1;
        } else if (this.p.y > renderer.height) {
            this.p.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        if (this.state != 2) {
            renderer.stroke(c2.Color.rgb(50, .2));
            renderer.lineWidth(2);
            renderer.fill(this.color);
            renderer.rect(this.p.x, this.p.y, this.randomWidth, this.randomHeight); // Draw rectangle with random width and height
        }
    }
}

// Function to generate neon or fluorescent colors
function randomNeonColor() {
    let neonColors = ['#ff00ff', '#00ffff', '#ffaa00', '#00ff00', '#ff00aa', '#ffff00', '#00ffaa', '#ffaa00', '#00aaff', '#aa00ff'];
    return neonColors[Math.floor(Math.random() * neonColors.length)];
}

let agents = [];

// Generate agents
for (let i = 0; i < 15; i++) {
    let x = random.next(renderer.width);
    let y = random.next(renderer.height);
    agents.push(new Agent(x, y));
}

let lastMouseMoveTime = 0;
const minMouseMoveInterval = 100; // milliseconds

// Define the draw function of the renderer
renderer.draw(() => {
    let voronoi = new c2.LimitedVoronoi();
    voronoi.compute(agents);

    // Display and update agents
    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});

// Register window resize event handler
window.addEventListener('resize', resize);
// Register mouse move event handler
window.addEventListener('mousemove', onMouseMove);

// Window resize function
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}

// Mouse move event function
function onMouseMove(event) {
    let currentTime = Date.now();
    if (currentTime - lastMouseMoveTime > minMouseMoveInterval) {
        let x = event.clientX;
        let y = event.clientY;
        agents.push(new Agent(x, y));
        lastMouseMoveTime = currentTime;
    }
}


// Second canvas code
// TAU is nicer than PI for trig
const TAU = Math.PI * 2;

// get canvas element & assign to 'cnv'
const secondCanvas = document.getElementById("secondCanvas");

// Define function for resizing canvas
function resize_canvas() {
    // Resize canvas to = viewport
    secondCanvas.width = innerWidth;
    secondCanvas.height = innerHeight;
}

// Assign to .onresize property of window
window.onresize = resize_canvas;

// Initialise canvas size
resize_canvas();

// Get canvas context & assign to 'ctx'
const ctx2 = secondCanvas.getContext('2d');

// Empty array for square objects to go in
const squuares = [];

// Assign to 'mouse_pos' a newly instantiated vector
const mouse_pos = new Vector(0, 0);

// Load ASCII art from file
let ascii_art;
fetch('ascii_art.txt')
    .then(response => response.text())
    .then(data => {
        ascii_art = data;
        // Split ASCII art into lines
        const lines = ascii_art.split('\n');
        // Draw ASCII art on canvas
        ctx2.fillStyle = 'black';
        ctx2.font = '6px monospace'; // Adjust font size here
        ctx2.textAlign = 'left';
        ctx2.textBaseline = 'top';
        // Draw each line of ASCII art
        lines.forEach((line, index) => {
            ctx2.fillText(line, 0, index * 6); // Adjust font size here
        });
        // Kick off the recursive animation sequence
        requestAnimationFrame(draw_frame);
    })
    .catch(error => console.error('Error loading ASCII art:', error));

// Whenever the pointer moves
secondCanvas.onpointermove = pointer_event => {
    // Update the x & y properties of 'mouse_pos' to
    // reflect the x & y properties of the pointer
    mouse_pos.x = pointer_event.x;
    mouse_pos.y = pointer_event.y;
};

// Whenever there is a touch or mouse click
secondCanvas.onpointerdown = pointer_event => {
    // Add an object to the squuares array, in which
    squuares.push({
        // The position = the x & y coordinates of the pointer
        p: new Vector(pointer_event.x, pointer_event.y),
        // The velocity = random direction w magnitude of 18
        v: vector_from_angle(Math.random() * TAU, 18)
    });
};

// Define the recursive animation sequence
function draw_frame() {
    // Clear canvas
    ctx2.clearRect(0, 0, secondCanvas.width, secondCanvas.height);

    // For each square in the 'squuares' array
    squuares.forEach(s => {
        // Random angle for nudge
        const nudge_angle = Math.random() * TAU;

        // Random magnitude for nudge
        const nudge_mag = Math.random() * 8;

        // Create nudge vector
        const nudge = vector_from_angle(nudge_angle, nudge_mag);

        // Nudge the square's position
        s.p.add(nudge);

        // Acceleration: start with a clone of 'mouse_pos'
        const acc = mouse_pos.clone();

        // Subtract the position of the square
        acc.subtract(s.p);

        // Set magnitude to 1
        acc.set_mag(1);

        // Add acceleration to the square's velocity
        s.v.add(acc);

        // If square's velocity is > 18, reduce to 18
        if (s.v.mag() > 18) s.v.set_mag(18);

        // Add velocity to the square's position
        s.p.add(s.v);

        // Draw the ASCII art at the position
        ctx2.fillStyle = 'white';
        ctx2.font = '6px monospace'; // Adjust font size here
        // Draw each line of ASCII art
        const lines = ascii_art.split('\n');
        lines.forEach((line, index) => {
            ctx2.fillText(line, s.p.x, s.p.y + (index * 6)); // Adjust font size here
        });
    });

    // Call the next frame
    requestAnimationFrame(draw_frame);
}
```
Ultimately, this code is net art with a 'glitch' theme. Randomly generated rectangles are responding to the glitch, with more rectangles being generated as the mouse moves. Additionally, the zany and confusing aesthetic is further emphasized through ASCII art that moves chaotically when you click the mouse.
