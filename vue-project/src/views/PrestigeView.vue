<template>
  <div class="prestige">
  <h3>Your Clicks: {{ clicked }}</h3>
  <h2>Prestige</h2>
  <button @click="prestige"> Click Me</button> 
  <h2>PP gain: {{ prestige_gain }}</h2>
  <h3>Cost: 1000000</h3>
  </div>
</template>
<script setup>
function prestige (){
  if (clicked.value >= 1000000){
    prestige_points = prestige_points + prestige_gain
    upgrade1_cost = 1
    upgrade2_cost = 100
    upgrade3_cost = 10000
    upgrade4_cost = 100000
    clicklyclicker = 1
    upgrade1.value = 1
    upgrade2.value = 1
    upgrade3.value = 0
    upgrade4.value = 1
  }else{
    console.log(clicked.value)
  }
}
</script>

<style>
@media (min-width: 1024px) {
}
</style>