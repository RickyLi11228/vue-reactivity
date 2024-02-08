<template>
  <h3>{{ clicked }}</h3>
  <button @click="increment">Click Me</button>
  <button @click="upgrader1">Click Me</button>
</template>
  
  <script setup>
  import { ref } from "vue";
  const props = defineProps({
    Destination: Object,
  });
  
  //clicker logic
  let clicked = ref(0);
  let clicklyclicker = 1
  function increment() {
    clicked.value = clicked.value + clicklyclicker;
    console.log(clicked.value)
  }
  let upgrade1 = ref(0)
  function upgrader1() {
    upgrade1.value = upgrade1.value + 1
    console.log(upgrade1.value)
  }
let clicklyclicker = clicklyclicker * upgrade1.value
  

  </script>
  
  <style scoped>
  img {
    width: 250px;
    height: 300px;
    object-fit: cover;
  }
  </style>