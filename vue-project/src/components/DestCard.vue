<template>
  <h3>{{ clicked }}</h3>
  <button @click="increment">Click Me</button>
  <h3>{{ upgrade1 }}</h3>
  <button @click="upgrader1">Click Me</button>
  <h3>Cost: {{ upgrade1_cost }}</h3>
</template>
  
  <script setup>
  import { ref } from "vue";
  const props = defineProps({
    Destination: Object,
  });
  
  //clicker logic
  let upgrade1_cost = 1
  const clicked = ref(0);
  let clicklyclicker = 1
  function increment() {
    clicked.value = clicked.value + clicklyclicker;
    console.log(clicked.value)
  }
  let upgrade1 = ref(1)
  function upgrader1() {
    if (upgrade1_cost <= clicked.value){
    upgrade1.value = upgrade1.value + 1
    console.log(upgrade1.value)
    clicklyclicker = 1 * upgrade1.value
    clicked.value = clicked.value - upgrade1_cost
    upgrade1_cost = upgrade1_cost * 2
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