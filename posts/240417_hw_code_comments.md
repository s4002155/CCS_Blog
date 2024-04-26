---
title: Example code comments, homework week 5
published_at: 2024-04-17
snippet: code comment example
disable_html_sanitization: true
---

<canvas id="glitch_self_portrait"></canvas>

<script type="module">

   const cnv = document.getElementById (`glitch_self_portrait`)
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16
   cnv.style.backgroundColor = `deeppink`

   const ctx = cnv.getContext (`2d`)

   let img_data

   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height)

   const img = new Image ()
   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      draw (img)
      img_data = cnv.toDataURL ("image/jpeg")
      add_glitch ()
   }
   img.src = `/240405/pfp_glasses.jpg`

   const rand_int = max => Math.floor (Math.random () * max)

   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4
      const i = rand_int (data.length - 24 - chunk_size) + 24
      const front = data.slice (0, i)
      const back = data.slice (i + chunk_size, data.length)
      const result = front + back
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }

   const glitch_arr = []

   const add_glitch = () => {
      const i = new Image ()
      i.onload = () => {
         glitch_arr.push (i)
         if (glitch_arr.length < 12) add_glitch ()
         else draw_frame ()
      }
      i.src = glitchify (img_data, 96, 6)
   }

   let is_glitching = false
   let glitch_i = 0

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i])
      else draw (img)

      const prob = is_glitching ? 0.05 : 0.02
      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length)
         is_glitching = !is_glitching
      }

      requestAnimationFrame (draw_frame)
   }

</script>

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