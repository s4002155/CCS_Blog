---
title: Create fractal using recursion and Canvas API.
published_at: 2024-03-28
snippet: week4 homework
disable_html_sanitization: true
---
<canvas id='fractal_tree'></canvas>

<script type='module'>
    const TAU = Math.PI * 2;

    // Function to create a vector from angle and magnitude
    function vectorFromAngle(angle, magnitude) {
        const x = magnitude * Math.cos(angle);
        const y = magnitude * Math.sin(angle);
        return { x, y };
    }

    const cnv = document.getElementById('fractal_tree');
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;
    const ctx = cnv.getContext('2d');

    // Function to generate a fractal tree
    function tree(base, stem, generation, options) {
        const end = {
            x: base.x + stem.x,
            y: base.y + stem.y
        };

        ctx.beginPath();
        ctx.moveTo(base.x, base.y);
        ctx.lineTo(end.x, end.y);
        ctx.stroke();

        if (generation > 0) {
            const leftStem = {
                x: stem.x * Math.cos(options.angle.l) - stem.y * Math.sin(options.angle.l),
                y: stem.x * Math.sin(options.angle.l) + stem.y * Math.cos(options.angle.l)
            };
            leftStem.x *= options.mult.l;
            leftStem.y *= options.mult.l;

            const rightStem = {
                x: stem.x * Math.cos(options.angle.r) - stem.y * Math.sin(options.angle.r),
                y: stem.x * Math.sin(options.angle.r) + stem.y * Math.cos(options.angle.r)
            };
            rightStem.x *= options.mult.r;
            rightStem.y *= options.mult.r;

            const nextGeneration = generation - 1;
            tree(end, leftStem, nextGeneration, options);
            tree(end, rightStem, nextGeneration, options);
        }
    }

    // Function to generate a new tree
    function newTree() {
        ctx.fillStyle = 'white';
        ctx.fillRect(0, 0, cnv.width, cnv.height);

        const options = {
            mult: {
                l: randBetween(0.5, 0.8),
                r: randBetween(0.5, 0.8)
            },
            angle: {
                l: randBetween(TAU / 12, TAU / 4) * -1,
                r: randBetween(TAU / 12, TAU / 4)
            }
        };

        const seed = { x: cnv.width / 2, y: cnv.height };
        const shoot = { x: 0, y: -150 };

        tree(seed, shoot, 8, options);
    }

    // Function to generate a random number between min and max
    function randBetween(min, max) {
        return min + Math.random() * (max - min);
    }

    cnv.onclick = newTree;
    newTree();
</script>

## Create a fractal using recursion

```
<canvas id='fractal_tree'></canvas>

<script type='module'>
    const cnv = document.getElementById ('fractal_tree')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    const ctx = cnv.getContext ('2d')

```
Firstly, I used Canvas API that provides a means for drawing graphics via JavaScript and the HTML element. So I started with ```document.getElementById()``` to get a reference to the canvas element and set its dimensions.

*To understand about the Canvas API, I refereced [this](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) page.*

```
<canvas id='fractal_tree'></canvas>

<script type='module'>
    // Define the constant representing two times pi
    const TAU = Math.PI * 2;

    // Function to create a vector from angle and magnitude
    function vectorFromAngle(angle, magnitude) {
        const x = magnitude * Math.cos(angle);
        const y = magnitude * Math.sin(angle);
        return { x, y };
    }

    const cnv = document.getElementById ('fractal_tree')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    const ctx = cnv.getContext ('2d')

```
*To understand how to make fractal tree by using recursion, I referenced the ['Recurtion' blog post](https://blog.science.family/240321_recursion).*

When I look through, I realized that in order to create a fractal tree, I had to use 'vectors'.

So I using ```function vectorFromAngle()``` to create  a vector from angle and magnitude.

```
// Function to generate a fractal tree
    function tree(base, stem, generation, options) {

        // Calculate the end point of the branch
        const end = {
            x: base.x + stem.x,
            y: base.y + stem.y
        };

        // Draw the branch
        ctx.beginPath();
        ctx.moveTo(base.x, base.y);
        ctx.lineTo(end.x, end.y);
        ctx.stroke();

        // Recursively generate branches
        if (generation > 0) {

             // Calculate left stem
            const leftStem = {
                x: stem.x * Math.cos(options.angle.l) - stem.y * Math.sin(options.angle.l),
                y: stem.x * Math.sin(options.angle.l) + stem.y * Math.cos(options.angle.l)
            };
            leftStem.x *= options.mult.l;
            leftStem.y *= options.mult.l;

            // Calculate right stem
            const rightStem = {
                x: stem.x * Math.cos(options.angle.r) - stem.y * Math.sin(options.angle.r),
                y: stem.x * Math.sin(options.angle.r) + stem.y * Math.cos(options.angle.r)
            };
            rightStem.x *= options.mult.r;
            rightStem.y *= options.mult.r;

            // Generate branches for next generation
            const nextGeneration = generation - 1;
            tree(end, leftStem, nextGeneration, options);
            tree(end, rightStem, nextGeneration, options);
        }
    }

```
Then I began the process of creating a fractal tree in earnest.

I used ```function tree()``` code to generate a fractal tree. I then tried to draw the branches of the fractal tree using code to calculate the endpoints of the branches and code to calculate the left and right stem.

*Detailed explanation is provided in the code description.*


```
 // Function to generate a new tree
    function newTree() {

        // Clear canvas
        ctx.fillStyle = 'white';
        ctx.fillRect(0, 0, cnv.width, cnv.height);

        // Generate options for tree generation
        const options = {
            mult: {
                l: randBetween(0.5, 0.8),
                r: randBetween(0.5, 0.8)
            },
            angle: {
                l: randBetween(TAU / 12, TAU / 4) * -1,
                r: randBetween(TAU / 12, TAU / 4)
            }
        };

        // Define seed and shoot vectors
        const seed = { x: cnv.width / 2, y: cnv.height };
        const shoot = { x: 0, y: -150 };

        // Generate the tree
        tree(seed, shoot, 8, options);
    }

    // Function to generate a random number between min and max
    function randBetween(min, max) {
        return min + Math.random() * (max - min);
    }

    // Call newTree function when canvas is clicked
    cnv.onclick = newTree;

    // Generate the initial tree
    newTree();
```

In the 'Recursion' blog that I referenced to create a fractal tree, I found a code that loads a new tree when clicked. To get some interesting results, I decided to create a fractal tree that would be randomly generated through clicks.

To achieve this result, I used the code ```function newTree()``` and started by initializing the canvas so that a new fractal tree can be created via ```ctx.fillStyle = 'white';```

And then, I generated code so that a new fractal tree would be randomly created each time I clicked. *Detailed explanation is provided in the code description.*

## Final code

```
<canvas id='fractal_tree'></canvas>

<script type='module'>
    const TAU = Math.PI * 2;

    // Function to create a vector from angle and magnitude
    function vectorFromAngle(angle, magnitude) {
        const x = magnitude * Math.cos(angle);
        const y = magnitude * Math.sin(angle);
        return { x, y };
    }

    const cnv = document.getElementById('fractal_tree');
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;
    const ctx = cnv.getContext('2d');

    // Function to generate a fractal tree
    function tree(base, stem, generation, options) {
        const end = {
            x: base.x + stem.x,
            y: base.y + stem.y
        };

        ctx.beginPath();
        ctx.moveTo(base.x, base.y);
        ctx.lineTo(end.x, end.y);
        ctx.stroke();

        if (generation > 0) {
            const leftStem = {
                x: stem.x * Math.cos(options.angle.l) - stem.y * Math.sin(options.angle.l),
                y: stem.x * Math.sin(options.angle.l) + stem.y * Math.cos(options.angle.l)
            };
            leftStem.x *= options.mult.l;
            leftStem.y *= options.mult.l;

            const rightStem = {
                x: stem.x * Math.cos(options.angle.r) - stem.y * Math.sin(options.angle.r),
                y: stem.x * Math.sin(options.angle.r) + stem.y * Math.cos(options.angle.r)
            };
            rightStem.x *= options.mult.r;
            rightStem.y *= options.mult.r;

            const nextGeneration = generation - 1;
            tree(end, leftStem, nextGeneration, options);
            tree(end, rightStem, nextGeneration, options);
        }
    }

    // Function to generate a new tree
    function newTree() {
        ctx.fillStyle = 'white';
        ctx.fillRect(0, 0, cnv.width, cnv.height);

        const options = {
            mult: {
                l: randBetween(0.5, 0.8),
                r: randBetween(0.5, 0.8)
            },
            angle: {
                l: randBetween(TAU / 12, TAU / 4) * -1,
                r: randBetween(TAU / 12, TAU / 4)
            }
        };

        const seed = { x: cnv.width / 2, y: cnv.height };
        const shoot = { x: 0, y: -150 };

        tree(seed, shoot, 8, options);
    }

    // Function to generate a random number between min and max
    function randBetween(min, max) {
        return min + Math.random() * (max - min);
    }

    cnv.onclick = newTree;
    newTree();
</script>
```
As a result, this is the complete code I generated to create a fractal tree.