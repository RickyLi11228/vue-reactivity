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
      img: "https://i.pinimg.com/736x/6c/1e/71/6c1e71b6338b0bf4e9ca8c0fc365d509.jpg",
    },
    {
      name: "Sliver Cursor",
      multiplier: 10,
      img: "https://atlas-content-cdn.pixelsquid.com/stock-images/symbol-cursor-arrow-silver-2JKw5K7-600.jpg",
    },
    {
      name: "Golden Cursor",
      multiplier: 25,
      img: "data:image/jpeg;base64,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"
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