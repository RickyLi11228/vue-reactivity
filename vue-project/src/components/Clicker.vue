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
  <h3>Upgrade 4: {{ upgrade4 }}</h3>
  <h2>Increase Clicked Exponent By 0.05</h2>
  <button @click="upgrader4">Click Me</button>
  <h3>Cost: {{ upgrade4_cost }}</h3>

  <h2>Prestige</h2>
  <h3>Your Prestige Points: {{ prestige_points }}</h3>
  <button @click="prestige"> Click Me</button> 
  <h2>PP gain: {{ prestige_gain }}</h2>
  <h3>Cost: 1000000</h3>
  
  <h2>Pets</h2>
  <button @click="pet">Click Me</button>
  <h3>Cost: 1 Prestige Point</h3>

  <h2>Your Total Pet Multiplier: {{pet_value}}</h2>
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
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT4g4yy2I0zTmvDA_xP4ctu3jUrQdZH2ZLzUA&usqp=CAU",
    },
    {
      name: "Sliver Cursor",
      multiplier: 10,
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS7r2_Au4cmXF_bUl_4VZnF7fr8nCnWhPgcJQ&usqp=CAU",
    },
    {
      name: "Golden Cursor",
      multiplier: 25,
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT3BjjuGO4Oz3UWJR--Xj2OghyRa6Vx1abBvQ&usqp=CAU"
    },
    {
      name: "Diamond Cursor",
      multiplier: 100,
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQh2XqeL4ucbFPpQv0J9EZ27YD4mGwNVaVAxg&usqp=CAU",
    }
  ]
  const inventory = []
function WhichPet(parameter) {
    DOMSelectors.pet_show.innerHTML="";
    parameter.forEach((thing) => {
        DOMSelectors.pet_show.insertAdjacentHTML(
            "beforeend",
            `<div class="card">
                <h3 class="name">You got the pet: ${thing.name}</h3>
                <img src="${thing.img} class="pet-img" alt="${thing.name} Picture">
                <h4>Multiplier: ${thing.multiplier}</h4>
            </div>`
        );
    });
}
   function value_update() {
    clicklyclicker = ((1 + upgrade3.value + pet_value.value) * upgrade1.value * upgrade2.value)** upgrade4.value
   }
  let upgrade1_cost = 1
  let upgrade2_cost = 100
  let upgrade3_cost = 10000
  let upgrade4_cost = 100000
  const clicked = ref(999999);
  let clicklyclicker = 1
  function increment() {
    clicked.value = clicked.value + clicklyclicker;
    prestige_gainer()
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
  let pet_value = ref(0);
  function pet_multiplier() {
    pet_value.value = 0;
    inventory.forEach((pet) => {
        pet_value.value += pet.multiplier;
    });
}
function pet(){
    if (prestige_points >= 1){
      prestige_points = prestige_points - 1
      const randomnumber = Math.floor(Math.random() * 10) + 1;
      console.log(randomnumber)
    if (randomnumber > 0 && randomnumber <= 4) {
      const which_pet = pets.find((pet) => pet.name === "Cursor")
        inventory.push(which_pet)
        WhichPet([which_pet]);
    } else if (randomnumber >= 5 && randomnumber <= 7) {
      const which_pet = pets.find((pet) => pet.name === "Sliver Cursor")
        inventory.push(which_pet)
        WhichPet([which_pet]);
    } else if (randomnumber === 8 || randomnumber === 9) {
      const which_pet = pets.find((pet) => pet.name === "Golden Cursor")
        inventory.push(which_pet)
        WhichPet([which_pet]);
    } else if (randomnumber === 10) {
      const which_pet = pets.find((pet) => pet.name === "Diamond Cursor")
        inventory.push(which_pet)
        WhichPet([which_pet]);
    }
    pet_multiplier();
    value_update();
  }
}
let prestige_gain = 0
function prestige_gainer(){
  prestige_gain = Math.round(clicked.value / 1000000)
}
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
      clicked.value = 0;
    }else{
      console.log(clicked.value)
    }
  }
    </script>
  
  <style scoped>
  .pet-img {
  width: 50px; 
  height: 50px; 
  object-fit: cover;
  }
  img {
    width: 250px;
    height: 300px;
    object-fit: cover;
  }
  </style>