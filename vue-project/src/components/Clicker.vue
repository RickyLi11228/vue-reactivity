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

  <button @click="insertPets">Show Pets</button>
  <h2>Pets</h2>
  <button @click="pet">Click Me</button>
  <h3>Cost: 1 Prestige Point</h3>
</template>
  
  <script setup>
  import { ref } from "vue";
  const props = defineProps({
    Destination: Object,
  });
  const DOMSelectors = {
    column: document.querySelector(".column"),
    pet_show: document.querySelector(".pet_show"),
}
  const pets = [
    {
      name: "Cursor",
      multiplier: 5,
      img: "",
    },
    {
      name: "Sliver Cursor",
      multiplier: 10,
      img: "",
    },
    {
      name: "Golden Cursor",
      multiplier: 25,
      img: "",
    },
    {
      name: "Diamond Cursor",
      multiplier: 100,
      img: "",
    }
  ]
  function clearfields(){
    DOMSelectors.column.innerHTML="";
}
  const inventory = []
  function insertPets(){
    DOMSelectors.pet_show.innerHTML="";
    show.forEach((thing) => {
        DOMSelectors.pet_show.insertAdjacentHTML(
            "beforeend",
            `<div class="card">
                <h3 class = "name">${thing.name}</h3>
                <img src="${thing.img}" class="img" alt="${thing.name} Picture">
                <h4>Multiplier: ${thing.multiplier}</h4> 
            </div>`
        )
    });
}
function WhichPet(parameter){
    clearfields();
    parameter.forEach((thing) => {
        DOMSelectors.pet_show.insertAdjacentHTML(
            "beforeend",
            `<div class="card">
                <h3 class = "name">${thing.name}</h3>
                <img src="${thing.img}" class="img" alt="${thing.name} Picture">
                <h4>Multiplier: ${thing.multiplier}</h4> 
            </div>`
        )
    });
}
   function value_update() {
    clicklyclicker = ((1 + upgrade3.value) * upgrade1.value * upgrade2.value)** upgrade4.value
   }
  let upgrade1_cost = 1
  let upgrade2_cost = 100
  let upgrade3_cost = 10000
  let upgrade4_cost = 100000
  const clicked = ref(999999);
  let clicklyclicker = 1
  function increment() {
    clicked.value = clicked.value + clicklyclicker;
  }
  let upgrade1 = ref(1)
  function upgrader1() {
    if (upgrade1_cost <= clicked.value){
    upgrade1.value = upgrade1.value + 1
    value_update()
    clicked.value = clicked.value - upgrade1_cost
    upgrade1_cost = upgrade1_cost * 3
    }
  }
  let upgrade2 = ref(1)
  function upgrader2() {
    if (upgrade2_cost <= clicked.value){
    upgrade2.value = upgrade2.value + 1
    value_update()
    clicked.value = clicked.value - upgrade2_cost
    upgrade2_cost = upgrade2_cost * 2
    }
  }
  let upgrade3 = ref(0)
  function upgrader3() {
    if (upgrade3_cost <= clicked.value){
    upgrade3.value = upgrade3.value + 10
    value_update()
    clicked.value = clicked.value - upgrade3_cost
    upgrade3_cost = upgrade3_cost * 2
    }
  }
  let upgrade4 = ref(1)
  function upgrader4() {
    if (upgrade4_cost <= clicked.value){
    upgrade4.value = upgrade4.value + 0.001
    value_update()
    clicked.value = clicked.value - upgrade4_cost
    upgrade4_cost = upgrade4_cost * 2
    }
  }
  let prestige_points = 10
  function pet_multiplier() {
    inventory.forEach((multi)=> clicklyclicker = clicklyclicker + multi);
  }
  function pet(){
    if (prestige_points >= 1){
      prestige_points = prestige_points - 1
      const randomnumber = Math.floor(Math.random() * 10) + 1;
      console.log(randomnumber)
    if (randomnumber > 0 && randomnumber <= 4) {
        inventory.push(5)
        let thing = pets[0]
        WhichPet(thing);
    } else if (randomnumber >= 5 && randomnumber <= 7) {
        inventory.push(10)
        let thing = pets[1]
        WhichPet(thing);
    } else if (randomnumber === 8 || randomnumber === 9) {
        inventory.push(25)
        let thing = pets[2]
        WhichPet(thing);
    } else if (randomnumber === 10) {
        inventory.push(100)
        let thing = pets[3]
        WhichPet(thing);
    }
    pet_multiplier()
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