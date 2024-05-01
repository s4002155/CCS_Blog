---
title: Create fractal using recursion and Canvas API.
published_at: 2024-03-28
snippet: week4 homework
disable_html_sanitization: true
---
<canvas id='fractal_tree_2'></canvas>

<script type='module'>
    const TAU = Math.PI * 2;

    // Function to create a vector from angle and magnitude
    function vectorFromAngle(angle, magnitude) {
        const x = magnitude * Math.cos(angle);
        const y = magnitude * Math.sin(angle);
        return { x, y };
    }

    const cnv = document.getElementById('fractal_tree_2');
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

    const cnv = document.getElementById ('fractal_tree')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    const ctx = cnv.getContext ('2d')

```

```
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

```

```
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
```

## Final code

```
<canvas id='fractal_tree_2'></canvas>

<script type='module'>
    const TAU = Math.PI * 2;

    // Function to create a vector from angle and magnitude
    function vectorFromAngle(angle, magnitude) {
        const x = magnitude * Math.cos(angle);
        const y = magnitude * Math.sin(angle);
        return { x, y };
    }

    const cnv = document.getElementById('fractal_tree_2');
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