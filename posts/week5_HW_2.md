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

```js
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

```js
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

```js
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

```js
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

```js
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
```js
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

## Discussion based on reading
### Which of Ngai's aesthetic categories does your self-portrait (and glitch more generally) belong to, and why?
In the three key aesthetic categories introduced in Sianne Ngai's book "Our Aesthetic Category: Zany, Cute, Interesting", my self-portrait (and glitch more generally) falls into the "Zany" category.

‘Zany’ refers to the absurd, chaotic, and unpredictable aspects of aesthetics. It encompasses elements that are whimsical, eccentric, or bizarre, often defying conventional expectations. From this perspective, glitches are chaotic, unpredictable, and random. That's why 'Zany', which  provoke laughter or amusement through their unconventional and unexpected nature, contains glitches.

### Does glitch increase or decrease effective complexity, and why?
From the perspective of "effective complexity", I think that the impact of a defect on complexity may depend on how the defect is perceived within a particular aesthetic frame.

First of all, from a general point of view, glitches can in some cases introduce unexpected and unpredictable elements into a system, increasing its effective complexity. Glitches create irregularities or deviations that disrupt the normal order or functioning of a system, adding to its complexity. These unexpected interruptions can increase effective complexity by prompting viewers to re-evaluate their understanding of the system and discover hidden patterns or relationships.

On the other hand, glitches can also reduce effective complexity by introducing excessive randomness or disorder into the system. If glitches make a system difficult or incomprehensible, they can reduce the ability to accurately describe or understand the structure or behavior of the system. In these cases, glitches can reduce the effective complexity of the system by obscuring underlying patterns or relationships and reducing overall consistency.

However, I believe that the impact of glitches on effective complexity may depend on their context and interpretation within a particular aesthetic frame. That's why, within the "Zany" category, I think glitches generally increase effective complexity.

First, glitches inherently introduce unpredictability and chaos into the system. This disrupts the expected order and functionality, adding complexity that wasn't there in the first place. This unpredictability increases effective complexity by forcing viewers to re-evaluate their understanding of the system.

Second, glitches often result in unexpected interactions between elements within a system. These interactions can create new patterns, behaviors, or visual effects that exceed existing expectations. The emergence of unexpected interactions adds depth and richness to the system, enhancing its overall complexity.

Finally, glitches invite viewers to engage with ambiguity and uncertainty. This disrupts existing ways of interpreting and perceiving, encouraging viewers to explore alternative ways of understanding the system. This engagement with ambiguity fosters curiosity and wonder, further increasing the effective complexity of flawed systems.

In other words, glitches within the “Zany” category increase effective complexity by introducing unpredictability, creating unexpected interactions, and leading viewers to ambiguity.