<template>
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <h2 v-bind:style="styleColor">Texto de color azul</h2>
  <p :style="styleFont">Fuente negrita </p>
  <h2>{{ arrayColores }}</h2>
  <h2>Color específico: `${arrayColores[2]}` </h2>

  <h2> {{ activo ? "Activo" : "Inactivo" }}</h2>

  <p v-if="activo">Estoy Activo</p>
  <p v-else>Estoy inactivo</p>
  <br>
  <ul>
    <li v-for="item of arrayElementos" :key="item">
      {{ item }}
    </li>
  </ul>
  <br>
  <ul>
    <li v-for="element in arrayOtherElements" :key="element.name">
      {{ element.name.toUpperCase() }} price {{ element.price }} description {{ element.description }}
    </li>
  </ul>

  <br>
  <ul>
    <li v-for="(it, prop) in objFruta" :key="it.id">
      {{ prop }} : {{  it }}
    </li>
  </ul>
  <button v-on:click="handleClick">Activame</button>

  <br>
  <button @click="increment">Incrementar</button>
  <h1 v-if="counter > 5" :style="{ color: 'blue'}">{{ counter }}</h1>
  <h1 v-else :style="{color:'red'}">{{ counter }}</h1>

  <br>
  <button v-on:click="incrementar">Incrementar</button>
  <button v-on:click="decrementar">Decrementar</button>
  <p>{{ counter2 }}</p>

  <br>
  <h1 :class="classCounter">{{ counter }}</h1>
  <br>
  <button v-on:click="add" :disabled="existItem">Add</button>
  <br>
  <p>{{ arrayFavoritos }}</p>
  <br>
  <ul>
    <li v-for="it in arrayFavoritos" :key="it">
      {{ it }}
    </li>
  </ul>
</template>


<script setup>

import {ref, computed} from 'vue';

  const name = "Vue Dinamico";
  const styleColor = "color: blue";
  const styleFont = "font-weight: bold";
  const arrayColores = ["red", "green", "blue"];
  const activo = true;

  const arrayElementos = ["uno", "dos", "tres"];

  const arrayOtherElements = [
    {
      name: "Elemento 1",
      price: "$1.00",
      description: "Description 1"
    },
    {
      name: "Elemento 2",
      price: "$2.00",
      description: "Description 2"
    },
    {
      name: "Elemento 3",
      price: "$3.00",
      description: "Description 3"
    }
  ];

  const objFruta = {
    name: "Manzana",
    price: "$1.00",
    description: "Description 1",
    id: 1
  }

  const handleClick = () => {
    console.log("Click");
  }
  
  const counter = ref(0);
  const increment = () => {
    counter.value ++;
  }

  const counter2 = ref(0);
  
  const incrementar = () => {
    counter2.value ++;
  }

  const decrementar = () => {
    counter2.value--;
  }

  const classCounter = computed(() => {
    if (counter.value === 0) {
      return 'zero';
    }

    if (counter.value > 0) {
      return 'positive';
    }

    if (counter.value < 0) {
      return 'negative';
    }

  });

  const arrayFavoritos = ref([]);

  const add = () => {
    arrayFavoritos.value.push(counter.value);
  }

  const existItem = computed(() => {
    const numSearched = arrayFavoritos.value.find(num => num === counter.value);

    if (numSearched === 0) {
      return true;
    }
    return numSearched
  })

</script>


<style>
  h1 {
    color: red;
  }
</style>