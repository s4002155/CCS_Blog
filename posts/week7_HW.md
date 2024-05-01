---
title: Combine with ideas from ascii cam
published_at: 2024-04-24
snippet: week7 homework
disable_html_sanitization: true
---
I tried combining [ascii cam](https://blog.science.family/240412_ascii_cam) with [c2.js ideas from week6](https://cold-koala-66.deno.dev/week6_HW_1).

<script src="/scripts/c2.min.js"></script>
<script src="/scripts/p5.js"></script>

<canvas id="c2"></canvas>
<div id="ascii_div"></div>


<!-- Code from [here](https://github.com/ren-yuan/c2.js/blob/main/examples/Delaunay.js) -->

<script>
//created by Ren Yuan

const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Point {
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }
}

let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();

const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"

const div = document.getElementById (`ascii_div`)
div.style.fontFamily = `monospace`
div.style.textAlign = `center`

renderer.draw(() => {
    renderer.clear();

    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    renderer.stroke(false);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }
    

    for (let i = 0; i < agents.length; i++) {
        agents[i].update();
    }

      const w = renderer.canvas.width
      const h = renderer.canvas.height
      const pixels = renderer.context.getImageData (0, 0, w, h).data

      let ascii_img = ``

      for (let y = 0; y < renderer.canvas.height; y += 22) {
         for (let x = 0; x < renderer.canvas.width; x += 10) {
            const i = (y * renderer.canvas.width + x) * 4
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]
            const br = (r * g * b / 16581376) ** 0.1
            const char_i = Math.floor (br * chars.length)
            ascii_img += chars[char_i]
         }
         ascii_img += `\n`
      }

      div.innerText = ascii_img
});

function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>

## Process
```html
<script src="/scripts/c2.min.js"></script>
<script src="/scripts/p5.js"></script>

<canvas id="c2"></canvas>


<!-- Code from [here](https://github.com/ren-yuan/c2.js/blob/main/examples/Delaunay.js) -->

<script>
//created by Ren Yuan

const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Point {
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        renderer.stroke('#333333');
        renderer.lineWidth(5);
        renderer.point(this.x, this.y);
    }
}

let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();


renderer.draw(() => {
    renderer.clear();

    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }
    

    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});


window.addEventListener('resize', resize);
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>
```
I decided to combine week6's c2.js ideas with ascii cam, so I started with the c2.js example used in week6.

```html
<script src="/scripts/c2.min.js"></script>
<script src="/scripts/p5.js"></script>

<canvas id="c2"></canvas>
<div id="ascii_div"></div>
```
By using ```<div></div>```, I created a div element with id "ascii_div"

```js
const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"; // Define a string of ASCII characters to represent grayscale values

const div = document.getElementById(`ascii_div`); // Get the div element with id "ascii_div"
div.style.fontFamily = `monospace`; // Set the font family of the div to monospace
div.style.textAlign = `center`; // Set the text alignment of the div to center
```
To combine with ascii cam, I wrote code referring to [this](https://blog.science.family/240412_ascii_cam) blog post.

```js
    renderer.stroke(false); // Disable stroke for drawing triangles
    for (let i = 0; i < triangles.length; i++) { // Loop through all triangles
        let t = c2.norm(triangles[i].area(), minArea, maxArea); // Normalize triangle area
        let color = c2.Color.hsl(30 * t, 30 + 30 * t, 20 + 80 * t); // Compute color based on normalized area
        renderer.fill(color); // Set fill color for the triangle
        renderer.triangle(triangles[i]); // Draw the triangle
    }

    for (let i = 0; i < agents.length; i++) { // Loop through all agents
    agents[i].update(); // Update agent position
    }
```
To avoid interfering with the creation of ascii characters, I disabled strokes for drawing triangles using the code ```renderer.stroke(false)```.

```js
 const w = renderer.canvas.width; // Get canvas width
    const h = renderer.canvas.height; // Get canvas height
    const pixels = renderer.context.getImageData(0, 0, w, h).data; // Get pixel data of canvas

    let ascii_img = ``; // Initialize variable to store ASCII art

    for (let y = 0; y < renderer.canvas.height; y += 22) { // Loop through canvas height with step size 22
        for (let x = 0; x < renderer.canvas.width; x += 10) { // Loop through canvas width with step size 10
            const i = (y * renderer.canvas.width + x) * 4; // Calculate index of pixel data
            const r = pixels[i]; // Get red component of pixel
            const g = pixels[i + 1]; // Get green component of pixel
            const b = pixels[i + 2]; // Get blue component of pixel
            const br = (r * g * b / 16581376) ** 0.1; // Calculate brightness of pixel
            const char_i = Math.floor(br * chars.length); // Map brightness to ASCII character index
            ascii_img += chars[char_i]; // Append ASCII character to ASCII art
        }
        ascii_img += `\n`; // Add newline character after each row
    }

    div.innerText = ascii_img; // Set inner text of div to ASCII art
```
Lastly, I finished writing code so that ascii cam can be applied to the existing c2.js example.


### Final code

```html
<script src="/scripts/c2.min.js"></script>
<script src="/scripts/p5.js"></script>

<canvas id="c2"></canvas>
<div id="ascii_div"></div>


<!-- Code from [here](https://github.com/ren-yuan/c2.js/blob/main/examples/Delaunay.js) -->

<script>
//created by Ren Yuan

const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Point {
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }
}

let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();

const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"

const div = document.getElementById (`ascii_div`)
div.style.fontFamily = `monospace`
div.style.textAlign = `center`

renderer.draw(() => {
    renderer.clear();

    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    renderer.stroke(false);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }
    

    for (let i = 0; i < agents.length; i++) {
        agents[i].update();
    }

      const w = renderer.canvas.width
      const h = renderer.canvas.height
      const pixels = renderer.context.getImageData (0, 0, w, h).data

      let ascii_img = ``

      for (let y = 0; y < renderer.canvas.height; y += 22) {
         for (let x = 0; x < renderer.canvas.width; x += 10) {
            const i = (y * renderer.canvas.width + x) * 4
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]
            const br = (r * g * b / 16581376) ** 0.1
            const char_i = Math.floor (br * chars.length)
            ascii_img += chars[char_i]
         }
         ascii_img += `\n`
      }

      div.innerText = ascii_img
});

function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>
```