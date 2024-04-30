---
title: Create fractal using recursion and Canvas API.
published_at: 2024-03-28
snippet: week4 homework
disable_html_sanitization: true
---

<canvas id='fractal_tree_1'></canvas>

<script type='module'>

    const cnv = document.getElementById ('fractal_tree_1')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    cnv.style.backgroundColor = `deeppink`

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