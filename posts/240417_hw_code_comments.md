---
title: Code comments
published_at: 2024-04-17
snippet: week 5 homework
disable_html_sanitization: true
---

## Glitch code comment

```html

<canvas id="glitch_self_portrait"></canvas>

<script type="module">


   //getting canvas element 
   const cnv = document.getElementById (`glitch_self_portrait`)

   //sizing to the good size
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16

   //setting background colour
   cnv.style.backgroundColor = `deeppink`

   // getting canvas context
   const ctx = cnv.getContext (`2d`)

   // instatiating variable for image data
   let img_data


   //defining a function that draws an image to the canvas
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height)

   // creating a new image element
   const img = new Image ()

   // define function to execute upon loading file
   img.onload = () => {

      //resizing the height of the canvas
      // to ba same aspect ratio as image
      cnv.height = cnv.width * (img.height / img.width)

      // drawing the image to the canvas
      draw (img)

      // storing image data as string in img_data
      img_data = cnv.toDataURL ("image/jpeg")

      // call the glitch function
      add_glitch ()
   }

   // give filepath to image element
   img.src = `/240405/pfp_glasses.jpg`
   
   // define a function that returns a random value between 0 - max
   const rand_int = max => Math.floor (Math.random () * max)

   // define a recursive function 
   const glitchify = (data, chunk_max, repeats) => {

      // random multiple of 4 between 0 - chunk_max
      const chunk_size = rand_int (chunk_max / 4) * 4

      // random position in the data between 24 - chunk_size
      const i = rand_int (data.length - 24 - chunk_size) + 24

      // grabbing all the daata before the random position
      const front = data.slice (0, i)

      // leaving a gap the size of chunk_size
      // grabbing the rest of the data
      const back = data.slice (i + chunk_size, data.length)

      // putting the two pieces back together
      // leaving out a chunk
      const result = front + back

      // ternary operator to return result if repeats = 0
      // otherwise call itself again with repeats - 1
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }

   // instantiate empty array for glitched images
   const glitch_arr = []

   // define funtion that adds a glitched image
   // to the glitch_arr array
   const add_glitch = () => {

      // make new image element
      const i = new Image ()

      // define function that executes when image recieves its data
      i.onload = () => {

         // push the image into the glitch_arr array
         glitch_arr.push (i)

         //call itself until there are 12 glitched images
         if (glitch_arr.length < 12) add_glitch ()

         // once there 12 images, start animating
         else draw_frame ()
      }

      // give the new image some glitchified image data
      i.src = glitchify (img_data, 96, 6)
   }

   // instantiate variable to keep track of glitch state
   let is_glitching = false

   // keep track of which glitched image from the array we are using
   let glitch_i = 0

   const draw_frame = () => {

      // check to see if we are glitching
      // if so, draw the glitched image form the array
      if (is_glitching) draw (glitch_arr[glitch_i])

      // otherwise draw the regular image
      else draw (img)

      // probability weightings for starting and stopping the glitch
      const prob = is_glitching ? 0.05 : 0.02

      // if random value is less than weighted value
      if (Math.random () < prob) {

         // choose a random glitched image index
         glitch_i = rand_int (glitch_arr.length)

         // flip the state of is_glitching
         is_glitching = !is_glitching
      }

      // call the next animation framegi
      requestAnimationFrame (draw_frame)
   }

</script>
```

## Pixel Sort code comment

```html
<canvas id="pixel_sort"></canvas>

<script type="module">
   import { PixelSorter } from "/scripts/pixel_sort.js"

   const cnv  = document.getElementById (`pixel_sort`)
   cnv.width  = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16   

   const ctx = cnv.getContext (`2d`)
   const sorter = new PixelSorter (ctx)

   const img = new Image ()

   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)
      sorter.init ()
      draw_frame ()
   }

   img.src = `/240408/kornerpark.jpg`

   let frame_count = 0
   const draw_frame = () => {

      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)

      let sig = Math.cos (frame_count * 2 * Math.PI / 500)

      const mid = {
         x: cnv.width / 2,
         y: cnv.height / 2
      }

      const dim = {
         x: Math.floor ((sig + 3) * (cnv.width / 6)) + 1,
         y: Math.floor ((sig + 1) * (cnv.height / 6)) + 1
      }

      const pos = {
         x: Math.floor (mid.x - (dim.x / 2)),
         y: Math.floor (mid.y - (dim.y / 2))
      }

      sorter.glitch (pos, dim)

      frame_count++
      requestAnimationFrame (draw_frame)
   }

</script>
```

```js
// pixel_sort.js

const quicksort = a => {
   if (a.length <= 1) return a

   let pivot = a[0]
   let left = []
   let right = []

   for (let i = 1; i < a.length; i++) {
      if (a[i].br < pivot.br) left.push (a[i])
      else right.push (a[i])
   }

   const sorted = [ ...quicksort (left), pivot, ...quicksort (right) ]

   return sorted
}

export class PixelSorter {
   constructor (ctx) {
      this.ctx = ctx
   }

   init () {
      this.width = this.ctx.canvas.width
      this.height = this.ctx.canvas.height
      this.img_data = this.ctx.getImageData (0, 0, this.width, this.height).data
   }


   glitch (pos, dim) {
      const find_i = c => ((c.y * this.ctx.canvas.width) + c.x) * 4 

      for (let x_off = 0; x_off < dim.x; x_off++) {
         const positions = []

         for (let y_pos = pos.y; y_pos < pos.y + dim.y; y_pos++) {
            positions.push (find_i ({ x: pos.x + x_off, y: y_pos }))
         }

         const unsorted = []

         positions.forEach (p => {
            const r = this.img_data[p]
            const g = this.img_data[p + 1]
            const b = this.img_data[p + 2]
            const a = this.img_data[p + 3]
            const br = r * g * b
            unsorted.push ({ r, g, b, a, br })
         })

         const sorted = quicksort (unsorted).reverse ()

         let rgba = []

         sorted.forEach (e => {
            rgba.push (e.r)
            rgba.push (e.g)
            rgba.push (e.b)
            rgba.push (e.a)
         })

         rgba = new Uint8ClampedArray (rgba)

         const new_data = this.ctx.createImageData (1, dim.y)
         
         new_data.data.set (rgba)

         this.ctx.putImageData (new_data, pos.x + x_off, pos.y)
      }
   }
}
```