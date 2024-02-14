<template>
  <h3>Your Clicks: {{ clicked }}</h3>
  <button @click="increment">Click Me</button>
  <h3>Upgrade 1: {{ upgrade1 }}</h3>
  <h2>Increase Clicked Gain By 100%</h2>
  <button @click="upgrader1">Click Me</button>
  <h3>Cost: {{ upgrade1_cost }}</h3>
  <h3>Upgrade 2: {{ upgrade2 }}</h3>
  <h2>Increase Clicked Gain By 200%</h2>
  <button @click="upgrader2">Click Me</button>
  <h3>Cost: {{ upgrade2_cost }}</h3>
  <h3>Upgrade 3: {{ upgrade3 }}</h3>
  <h2>Increase Base Clicked Value By 10</h2>
  <button @click="upgrader3">Click Me</button>
  <h3>Cost: {{ upgrade3_cost }}</h3>
  <h2>Increase Clicked Exponent By 0.05</h2>
  <button @click="upgrader4">Click Me</button>
  <h3>Cost: {{ upgrade4_cost }}</h3>
  <h2>Prestige</h2>
  <button @click="prestige">Click Me</button> <h2> PP gain: {{ prestige_gain }}</h2>
  <h3>Cost: 1000000</h3>
</template>
  
  <script setup>
  import { ref } from "vue";
  const props = defineProps({
    Destination: Object,
  });
  const DOMSelectors = {
    column: document.querySelector(".column"),
  }
  let prestige_gain = clicked.value/1000000
function prestige (){
  if (clicked.value > 1000000){
    prestige_points = prestige_point + prestige_gain
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
  let upgrade1_cost = 1
  let upgrade2_cost = 100
  let upgrade3_cost = 10000
  let upgrade4_cost = 100000
  const clicked = ref(1000000);
  let clicklyclicker = 1
  function increment() {
    clicked.value = clicked.value + clicklyclicker;
  }
  let upgrade1 = ref(1)
  function upgrader1() {
    if (upgrade1_cost <= clicked.value){
    upgrade1.value = upgrade1.value + 1
    clicklyclicker = ((1 + upgrade3.value) * upgrade1.value * upgrade2.value)** upgrade4.value
    clicked.value = clicked.value - upgrade1_cost
    upgrade1_cost = upgrade1_cost * 3
    }
  }
  let upgrade2 = ref(1)
  function upgrader2() {
    if (upgrade2_cost <= clicked.value){
    upgrade2.value = upgrade2.value + 1
    clicklyclicker = ((1 + upgrade3.value) * upgrade1.value * upgrade2.value)** upgrade4.value
    clicked.value = clicked.value - upgrade2_cost
    upgrade2_cost = upgrade2_cost * 2
    }
  }
  let upgrade3 = ref(0)
  function upgrader3() {
    if (upgrade3_cost <= clicked.value){
    upgrade3.value = upgrade3.value + 10
    clicklyclicker = ((1 + upgrade3.value) * upgrade1.value * upgrade2.value)** upgrade4.value
    clicked.value = clicked.value - upgrade3_cost
    upgrade3_cost = upgrade3_cost * 2
    }
  }
  let upgrade4 = ref(1)
  function upgrader4() {
    if (upgrade4_cost <= clicked.value){
    upgrade4.value = upgrade4.value + 0.001
    clicklyclicker = ((1 + upgrade3.value) * upgrade1.value * upgrade2.value)** upgrade4.value
    clicked.value = clicked.value - upgrade4_cost
    upgrade4_cost = upgrade4_cost * 2
    }
  }
  
  </script>
  
  <style scoped>
  img {
    width: 250px;
    height: 300px;
    object-fit: cover;
  }
  </style>