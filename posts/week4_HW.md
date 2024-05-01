---
title: Create fractal using recursion and Canvas API.
published_at: 2024-03-28
snippet: week4 homework
disable_html_sanitization: true
---
Test text
<canvas id='fractal_tree_1'></canvas>

<script type='module'>

    const TAU = Math.PI * 2

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

    mag () { // using a^2 + b^2 = c^2
        return ((this.x ** 2) + (this.y ** 2)) ** 0.5
    }

    setMag (m) {
        this.mult (m / this.mag ())
    }

    rotate (a) {
        // from "Formula for rotating a vector in 2D" by Matthew Brett
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

    const cnv = document.getElementById ('fractal_tree_1')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16

    const ctx = cnv.getContext ('2d')

    // define a function to return a random value
    // between a minimum and maximum
    function rand_between (min, max) {
        const dif = max - min
        const off = Math.random () * dif
        return  min + off
    }

    // this function has been modified to recieve 
    // an options object housing angle and mult data
    function tree (base, stem, generation, options) {
        const end = base.clone ()
        end.add (stem)

        ctx.beginPath ()
        ctx.moveTo (base.x, base.y)
        ctx.lineTo (end.x, end.y)
        ctx.stroke ()


        if (generation > 0) {
            const L_stem = stem.clone ()

            // use the data in the options object
            // for the left angle
            L_stem.rotate (options.angle.l)

            // for the left multiplier
            L_stem.mult (options.mult.l)

            const R_stem = stem.clone ()

            // for the right angle
            R_stem.rotate (options.angle.r)

            // and for the right multiplier
            R_stem.mult (options.mult.r)

            const next_gen = generation - 1

            // pass the options object
            // on to the next generation
            tree (end, L_stem, next_gen, options)
            tree (end, R_stem, next_gen, options)
        }
    }

    const seed = new Vector (cnv.width / 2, cnv.height)
    const shoot = new Vector (0, -150)

    // function for a new tree
    function new_tree () {

        // clear the canvas
        ctx.fillStyle = `white`
        ctx.fillRect (0, 0, cnv.width, cnv.height)

        // create an options object
        // using object literal notation
        const options = {
            mult : {
                l : rand_between (0.5, 0.8),
                r : rand_between (0.5, 0.8),
            },

            angle : {
                l : rand_between (TAU / 12, TAU / 4) * -1,
                r : rand_between (TAU / 12, TAU / 4),
            }
        }

        // grow a tree using the options generated
        tree (seed, shoot, 8, options)
    }

    // assign the new_tree function to the 
    // .onclick property of the canvas
    cnv.onclick = new_tree

    // make a tree
    new_tree ()
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

```
<canvas id='fractal_tree'></canvas>

<script type='module'>
    const cnv = document.getElementById ('fractal_tree')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    const ctx = cnv.getContext ('2d')

    function tree (base, stem, generation) {

    }

```

<canvas id="fractal_tree_canvas"></canvas>

<script>
    // Get the canvas element and its context
    const canvas = document.getElementById('fractal_tree_canvas');
    const ctx = canvas.getContext('2d');

    // Set canvas dimensions
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    // Define parameters for the fractal tree
    const startX = canvas.width / 2;
    const startY = canvas.height;
    const trunkLength = 150;
    const trunkWidth = 10;
    const branchAngle = Math.PI / 4;
    const branchLengthRatio = 0.7;
    const branchWidthRatio = 0.7;
    const maxDepth = 6;

    // Function to draw a branch
    function drawBranch(x, y, length, angle, width, depth) {
        if (depth === 0) return;

        // Calculate the endpoint of the branch
        const endX = x + Math.cos(angle) * length;
        const endY = y - Math.sin(angle) * length;

        // Draw the branch
        ctx.beginPath();
        ctx.moveTo(x, y);
        ctx.lineTo(endX, endY);
        ctx.lineWidth = width;
        ctx.strokeStyle = '#663300'; // Brown color
        ctx.stroke();

        // Recursively draw the left and right branches
        drawBranch(endX, endY, length * branchLengthRatio, angle - branchAngle, width * branchWidthRatio, depth - 1);
        drawBranch(endX, endY, length * branchLengthRatio, angle + branchAngle, width * branchWidthRatio, depth - 1);
    }

    // Draw the fractal tree
    function drawTree() {
        // Clear the canvas
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        // Draw the trunk
        ctx.beginPath();
        ctx.moveTo(startX - trunkWidth / 2, startY);
        ctx.lineTo(startX + trunkWidth / 2, startY);
        ctx.lineWidth = trunkWidth;
        ctx.strokeStyle = '#663300'; // Brown color
        ctx.stroke();

        // Draw the branches recursively
        drawBranch(startX, startY - trunkLength, trunkLength * branchLengthRatio, -Math.PI / 2, trunkWidth * branchWidthRatio, maxDepth);
    }

    // Redraw the tree when the window is resized
    window.addEventListener('resize', function () {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        drawTree();
    });

    // Draw the initial tree
    drawTree();
</script>
