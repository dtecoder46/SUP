<script setup>

  function high_diff(hue, saturation, lightness, diff, max, Rp, Gp, Bp) {
    saturation = 100 // this helps create the final, highly saturated color output

    if (max == Rp) {
      hue = 60 * (((Gp - Bp)/diff) % 6)
    }

    if (max == Gp) {
      hue = 60 * (((Bp - Rp)/diff) + 2)
    }

    if (max == Bp) {
      hue = 60 * (((Rp - Gp)/diff) + 4)
    }

    const hsl_str = "hsl(" + hue + "deg " + saturation + "% " + lightness + "%)"

    document.getElementById("SUP").style.backgroundColor = hsl_str
  }

  function HSL() {
    const R = document.getElementById("red").value
    const G = document.getElementById("green").value
    const B = document.getElementById("blue").value

    document.getElementById("input_color").style.backgroundColor = "rgb(" + R + "," + G + "," + B + ")"

    const Rp = R/255
    const Gp = G/255
    const Bp = B/255

    const max = Math.max(Rp, Gp, Bp)
    const min = Math.min(Rp, Gp, Bp)

    const diff = max - min

    const lightness = ((max + min)/2) * 100

    let hue

    let saturation

    if (diff == 0) {
      hue = 0
      saturation = 0
    }

    if (diff != 0) {
      high_diff(hue, saturation, lightness, diff, max, Rp, Gp, Bp)
    }
    
  }
</script>

<template>
  <div id="SUP">
    <img src="public/sup_logo.jpg" class="absolute w-16 h-24 m-5"><br><br><br><br><br><br>
    <div id="color_in">
      <div id="input_color" class="absolute w-20 h-20 rounded-xl border-2 border-black border-solid shadow-md shadoow-gray-400 ml-5"></div><br><br><br><br>
      
      <p class="absolute w-10 h-6 not-italic font-normal text-2xl leading-6 text-black ml-5">RED:</p><br>
      <input type="text" id="red" class="absolute w-16 h-5 bg-red-300 rounded-xl ml-5"><br>

      <p class="absolute w-16 h-6 not-italic font-normal text-2xl leading-6 text-black ml-5">GREEN:</p><br>
      <input type="text" id="green" class="absolute w-16 h-5 bg-green-200 rounded-xl ml-5"><br>

      <p class="absolute w-16 h-6 not-italic font-normal text-2xl leading-6 text-black ml-5">BLUE:</p><br>
      <input type="text" id="blue" class="bg-indigo-300 absolute w-16 h-5 bg-green-200 rounded-xl ml-5"><br><br>
    </div>

    <button @click="HSL()" class="box-border absolute w-20 h-10 text-2xl bg-teal-100 rounded-xl border-solid border-black border-2 shadow-md shadow-teal-100 ml-5">SUBMIT</button><br><br><br><br>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Jersey+10&display=swap');

.jersey-10-regular {
  font-family: "Jersey 10", sans-serif;
  font-weight: 400;
  font-style: normal;
}

#SUP {
  font-family: "Jersey 10"
}

</style>
