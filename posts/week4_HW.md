---
title: Create fractal using recursion and Canvas API.
published_at: 2024-03-28
snippet: week4 homework
disable_html_sanitization: true
---

<canvas id='fractal_tree_0'></canvas>

<script type='module'>

    // get and format canvas
    const cnv = document.getElementById ('fractal_tree_0')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16

    // get canvas context
    const ctx = cnv.getContext ('2d')

    // this is the recursive function that will draw the tree
    // it accepts three arguments:
    // base: vector describing the starting position
    // stem: vector describing the new line
    // generation: integer limiting the number of recursions
    function tree (base, stem, generation) {

        // start with the base position
        // we want to tranform it, so we make a copy
        const end = base.clone ()

        // add the stem to the start position
        end.add (stem)

        // draw the line from the start point
        // to the end point
        ctx.beginPath ()
        ctx.moveTo (base.x, base.y)
        ctx.lineTo (end.x, end.y)
        ctx.stroke ()

        // if generations is still positive
        if (generation > 0) {

            // clone the stem
            const L_stem = stem.clone ()

            // rotate it anti-clockwise
            L_stem.rotate (-TAU / 7)

            // reduce the length
            L_stem.mult (0.6)

            // clone the stem again
            const R_stem = stem.clone ()

            // rotate this one clockwise
            R_stem.rotate (TAU / 7)

            // reduce its length
            R_stem.mult (0.6)

            // decrease generation by 1
            const next_gen = generation - 1

            // recursively call tree twice, 
            // with end as the new base
            // L_stem & R_stem as the new stems
            // and next_gen as the new generation
            tree (end, L_stem, next_gen)
            tree (end, R_stem, next_gen)
        }
    }

    // new vector defining the starting point of our tree
    const seed = new Vector (cnv.width / 2, cnv.height)

    // new vector defining the first stem
    // ie. 150 pixels straight up
    const shoot = new Vector (0, -150)

    // pass seed in as the base argument
    // shoot as the stem argument
    // and 7, denoting that we want 7 recursions
    tree (seed, shoot, 7)
</script>