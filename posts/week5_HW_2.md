---
title: Self-portrait in the style of glitch
published_at: 2024-04-12
snippet: Second Homework for W5
disable_html_sanitization: true
---

<div align="center">
<iframe src="https://s4002155-blank-net-a-59.deno.dev/" width="600px" height="800px"></iframe>
</div>

## Using blacnk_net_art template

``` index.html
<!doctype html>
<head>
    <title> b l a n k </title>
</head>

<body>
   <canvas id="cnv_element"></canvas>
   <script type="module" src="script.js"></script>
</body>
```

This template consists of two parts. In the code consisting of "index.html" and "script.js", I will write the code in "script.js".

```
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

This is the existing code in script.js.


## Glitch code in script.js
```
// Set margin and overflow properties of the body to 0 and 'hidden' respectively
document.body.style.margin = 0;
document.body.style.overflow = 'hidden';

// Get the canvas element and set its initial width and height to match the window inner dimensions
const cnv = document.getElementById('cnv_element');
cnv.width = innerWidth;
cnv.height = innerHeight;

// Get the 2D rendering context of the canvas
const ctx = cnv.getContext('2d');

// Ensure the canvas resizes appropriately when the window is resized
window.onresize = () => {
    cnv.width = innerWidth;
    cnv.height = innerHeight;
};
```
First, I started by creating a canvas.

```
// Set margin and overflow properties of the body to 0 and 'hidden' respectively
document.body.style.margin = 0;
document.body.style.overflow = 'hidden';

// Get the canvas element and set its initial width and height to match the window inner dimensions
const cnv = document.getElementById('cnv_element');
cnv.width = innerWidth;
cnv.height = innerHeight;

// Get the 2D rendering context of the canvas
const ctx = cnv.getContext('2d');

// Ensure the canvas resizes appropriately when the window is resized
window.onresize = () => {
    cnv.width = innerWidth;
    cnv.height = innerHeight;
    // Redraw the image to fit the new canvas dimensions
    draw_image();
};

// Variable to hold the encoded image data
let img_data;

// Create a new image object
const img = new Image();
// Load event listener for the image
img.onload = () => {
    // Draw the image on the canvas
    draw_image();
    // Convert the canvas content to base64 encoded image data
    img_data = cnv.toDataURL('image/jpeg');
    // Apply glitch effect to the image
    add_glitch();
};
// Set the source of the image
img.src = 'image.jpg';

console.dir(img);
```
In order to create code that causes glitches in the image, I first wrote code to load the image.

```
document.body.style.margin   = 0;
document.body.style.overflow = 'hidden';

const cnv = document.getElementById('cnv_element');
cnv.width = innerWidth;
cnv.height = innerHeight;

const ctx = cnv.getContext('2d');

// Function to draw the image on the canvas
const draw_image = () => {
   const scale = Math.min(cnv.width / img.width, cnv.height / img.height);
   const offsetX = (cnv.width - img.width * scale) / 2;
   const offsetY = (cnv.height - img.height * scale) / 2;
   ctx.drawImage(img, offsetX, offsetY, img.width * scale, img.height * scale);
};

// Ensure canvas resizes when window is resized
window.onresize = () => {
   cnv.width = innerWidth;
   cnv.height = innerHeight;
   draw_image();
};

let img_data;

// Load the image and draw it on the canvas
const img = new Image();
img.onload = () => {
   draw_image();
   img_data = cnv.toDataURL('image/jpeg');
   add_glitch();
};
img.src = 'image.jpg';

console.dir(img);
```
Since I only wrote code to load the image, the image will not be displayed on the screen. To draw the image on the canvas, I will display it on the screen through ```const draw_image = () => {```.

```
const rand_int = max => Math.floor(Math.random() * max);

const glitchify = (data, chunk_max, repeats) => {
   const chunk_size = rand_int(chunk_max / 4) * 4;
   const i = rand_int(data.length - 24 - chunk_size) + 24;
   const front = data.slice(0, i);
   const back = data.slice(i + chunk_size, data.length);
   const result = front + back;
   return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
};

const glitch_arr = [];

const add_glitch = () => {
   const i = new Image();
   i.onload = () => {
      glitch_arr.push(i);
      if (glitch_arr.length < 12) add_glitch();
      else draw_frame();
   };
   i.src = glitchify(img_data, 96, 6);
};

let is_glitching = false;
let glitch_i = 0;

const draw_frame = () => {
   if (is_glitching) draw(glitch_arr[glitch_i]);
   else draw(img);

   const prob = is_glitching ? 0.05 : 0.02;
   if (Math.random() < prob) {
      glitch_i = rand_int(glitch_arr.length);
      is_glitching = !is_glitching;
   }

   requestAnimationFrame(draw_frame);
};
```
Then I started writing glitch code in earnest. *Code referenced from ['Glitch' blog post](https://blog.science.family/240405_glitch).*

```
// Function to draw an image on the canvas with original dimensions
const draw = i => {
    // Calculate the scaling factor for the image
    const scale = Math.min(cnv.width / i.width, cnv.height / i.height);
    // Calculate the offset to center the image on the canvas
    const offsetX = (cnv.width - i.width * scale) / 2;
    const offsetY = (cnv.height - i.height * scale) / 2;
    // Draw the image on the canvas with the calculated parameters
    ctx.drawImage(i, offsetX, offsetY, i.width * scale, i.height * scale);
};
```
Because the size of the canvas was set to the screen size, the image size was adjusted to the screen size, causing a problem where only part of the image was visible. To solve this, I ended up writing code to draw the image on the canvas at its original size.

## Final code
```script.js
document.body.style.margin   = 0;
document.body.style.overflow = 'hidden';

const cnv = document.getElementById('cnv_element');
cnv.width = innerWidth;
cnv.height = innerHeight;

const ctx = cnv.getContext('2d');

// Function to draw the image on the canvas
const draw_image = () => {
   const scale = Math.min(cnv.width / img.width, cnv.height / img.height);
   const offsetX = (cnv.width - img.width * scale) / 2;
   const offsetY = (cnv.height - img.height * scale) / 2;
   ctx.drawImage(img, offsetX, offsetY, img.width * scale, img.height * scale);
};

// Ensure canvas resizes when window is resized
window.onresize = () => {
   cnv.width = innerWidth;
   cnv.height = innerHeight;
   draw_image();
};

let img_data;

// Load the image and draw it on the canvas
const img = new Image();
img.onload = () => {
   draw_image();
   img_data = cnv.toDataURL('image/jpeg');
   add_glitch();
};
img.src = 'image.jpg';

console.dir(img);

const rand_int = max => Math.floor(Math.random() * max);

const glitchify = (data, chunk_max, repeats) => {
   const chunk_size = rand_int(chunk_max / 4) * 4;
   const i = rand_int(data.length - 24 - chunk_size) + 24;
   const front = data.slice(0, i);
   const back = data.slice(i + chunk_size, data.length);
   const result = front + back;
   return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
};

const glitch_arr = [];

const add_glitch = () => {
   const i = new Image();
   i.onload = () => {
      glitch_arr.push(i);
      if (glitch_arr.length < 12) add_glitch();
      else draw_frame();
   };
   i.src = glitchify(img_data, 96, 6);
};

let is_glitching = false;
let glitch_i = 0;

const draw_frame = () => {
   if (is_glitching) draw(glitch_arr[glitch_i]);
   else draw(img);

   const prob = is_glitching ? 0.05 : 0.02;
   if (Math.random() < prob) {
      glitch_i = rand_int(glitch_arr.length);
      is_glitching = !is_glitching;
   }

   requestAnimationFrame(draw_frame);
};

// Function to draw an image on the canvas with original dimensions
const draw = i => {
   const scale = Math.min(cnv.width / i.width, cnv.height / i.height);
   const offsetX = (cnv.width - i.width * scale) / 2;
   const offsetY = (cnv.height - i.height * scale) / 2;
   ctx.drawImage(i, offsetX, offsetY, i.width * scale, i.height * scale);
};
```
