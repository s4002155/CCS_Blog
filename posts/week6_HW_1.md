---
title: Implementing example of c2.js in the blog
published_at: 2024-04-17
snippet: First Homework for W6
disable_html_sanitization: true
---

Code from [here](https://github.com/ren-yuan/c2.js/blob/main/examples/Delaunay.js)

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

### CODE

```html
<!-- Include the c2.js library -->
<script src="/scripts/c2.min.js"></script>
<!-- Include the p5.js library -->
<script src="/scripts/p5.js"></script>

<!-- Create a canvas element with id 'c2' -->
<canvas id="c2"><//canvas>

<script>
//created by Ren Yuan

// Initialize a renderer using c2.Renderer with the canvas element 'c2'
const renderer = new c2.Renderer(document.getElementById('c2'));

// Call the resize function to set initial size
resize();

// Set the background color of the renderer
renderer.background('#cccccc');

// Create a random number generator
let random = new c2.Random();

// Define a class Agent which inherits from c2.Point
class Agent extends c2.Point {
    constructor() {
        // Initialize x and y coordinates with random values within the renderer dimensions
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        // Initialize velocity components with random values between -2 and 2
        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    // Method to update the position of the agent
    update() {
        this.x += this.vx;
        this.y += this.vy;

        // Bounce off the edges of the canvas
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

    // Method to display the agent as a point
    display() {
        renderer.stroke('#333333');
        renderer.lineWidth(5);
        renderer.point(this.x, this.y);
    }
}

// Create an array of 20 agents
let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();

// Define a drawing function for the renderer
renderer.draw(() => {
    // Clear the renderer
    renderer.clear();

    // Create a Delaunay triangulation object
    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    // Calculate maximum and minimum triangle areas
    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    // Draw triangles with colors based on normalized areas
    renderer.stroke('#333333');
    renderer.lineWidth(1);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }

    // Display and update all agents
    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});

// Add a resize event listener to adjust canvas size
window.addEventListener('resize', resize);
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>
```
