<template>
  <!-- interpolación de texto -->
  <div class="container mt-2">
    <h1>Interpolación de texto</h1>
    <h2>Hello {{ name.toUpperCase() }}</h2>
    <hr>
  </div>
  <!-- Enlaces de atributos -->
  <div class="container mt-2">
    <h1>Enlaces de atributos</h1>
    <h2 :style="styleColor">Soy Azul</h2>
    <hr>
  </div>
  <!-- Uso de expresiones de JavaScript -->
  <div class="container mt-2">
    <h1>Uso de expresiones de JavaScrip</h1>
    <h3 :style="styleColorArray">{{ arrayColores }}</h3>
    <h3 :style="`color: ${arrayColores[1]}`">Soy color green</h3>
    <hr>
  </div>

  <!-- Directivas -->
  <div class="container mt-2">
    <h1>Directivas</h1>
    <!-- Las directivas son atributos especiales con el prefijo v- -->
    <h2>{{ activo ? 'Estoy en true' : 'Estoy en false' }}</h2>
  </div>
  <!-- v-if | v-else | v-show -->
  <div class="container mt-2">
    <h1>v-if | v-else | v-show</h1>
    <h3 v-if="activo">Estoy en activo</h3>
    <h3 v-else>Estoy en inactivo</h3>
    <p v-if="activo === true">Estoy activo</p>
    <p v-else-if="activo === false">Estoy inactivo</p>
    <p v-else>Estoy indeciso</p>
    <h2 v-show="activo">Estoy activo v-show</h2>
    <hr>
  </div>

  <!-- v-for -->
  <div class="container mt-2">
    <h1>v-for</h1>
    {{ arrayFrutas }}
    <!-- Por cada v-for que hagamos en nuestro sitio web vamos a tener que pasarle un identificador único que va a recibir la :key -->
    <ul>
      <li v-for="(fruta, index) in arrayFrutas" :key="index">
        {{ fruta }}
      </li>
    </ul>
    <ul>
      <!-- <li v-for="fruta in arrayFrutas" :key="name">
            {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
        </li> -->
      <li v-for="(frutas, name) in arrayFrutasObject" :key="name">
        {{ frutas.name }} - {{ frutas.price }} - {{ frutas.description }}
      </li>
    </ul>
    {{ objetoFruta }}
    <ul>
      <!-- <li v-for="value in objetoFruta" :key="value">
      {{ value }}
    </li> -->
      <li v-for="(value, propiedad, index) in objetoFruta" :key="value">
        {{ index }} - {{ propiedad }} - {{ value }}
      </li>
    </ul>
    <hr>

  </div>
  <!-- v-for v-if -->
  <div class="container mt-2">
    <h1>v-for v-if</h1>
    {{ arrayFrutasVifVfor }}
    <ul>
      <template v-for="item in arrayFrutasVifVfor" :key="item.name">
        <li v-if="item.stock > 0">
          {{ item.name }} - {{ item.price }}
        </li>
      </template>
      <!-- <li 
   v-for="item in arrayFrutasVifVfor" 
  :key="item.name"> -->
      <!-- Alternativa  pero no recomandada-->
      <!-- <span v-if="item.stock > 0">
    {{ item.name }} - {{ item.price }}
  </span>
  </li> -->
    </ul>
    <hr>
  </div>
  <!-- v-on -->
  <div class="container mt-2">
    <h1>v-on</h1>
    <div class="text-center btn-group">
      <!-- Podemos usar la directiva v-on, que normalmente acortamos al símbolo @, para escuchar eventos DOM y ejecutar JavaScript cuando se activan. El uso sería v-on:click="handler" o con el atajo, @click="handler". -->
      <button v-on:click.right.prevent="handleClick('Texto right')" class="btn btn-success">Activame clic right
        v-on:click</button>
      <button @click.left="handleClick('Texto left')" class="btn btn-danger">Activame clic left @click</button>
      <button @click.middle="handleClick('Texto middle')" class="btn btn-secondary">Activame clic middle @click</button>
    </div>
    <hr>
  </div>

  <!-- Reactividad -->
  <div class="container mt-2">
    <h1>Reactividad</h1>
    <div class="text-center btn-group">
      <button @click="incrementA" class="btn btn-success">Aumentar</button>
      <button @click="resetA" class="btn btn-danger">Reset</button>
      <button @click="decrementA" class="btn btn-secondary">Disminuir</button>
    </div>
    <h2 :class="counterA > 0 ? 'colorMayorA' : 'colorMenorB'">{{ counterA }}</h2>
    <hr>
  </div>
  <!-- Computed -->
  <div class="container mt-2 text-center">
    <h1>Computed</h1>
    <div class="text-center btn-group">
      <button @click="incrementB" class="btn btn-success">Aumentar</button>
      <button @click="resetB" class="btn btn-danger">Reset</button>
      <button @click="decrementB" class="btn btn-secondary">Disminuir</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add List</button>
    </div>
    <h2 :class="classCounter">{{ counterB }}</h2>
    <!-- {{ addList }} -->
    <ul class="list-group mt-4">
      <li v-for="(list, index) in addList" :key="index" class="list-group-item">
        {{ list }}
      </li>
    </ul>
  </div>
</template>



<script setup>
import { computed, ref } from 'vue'

const name = 'Vue3 desde script setup'

const styleColor = 'color:blue'
const styleColorArray = 'color:peru'
const arrayColores = ['blue', 'green', 'yellow', 'orange']

const activo = true

const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];

const arrayFrutasObject = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
  },
];

const objetoFruta = {
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana",
}

const arrayFrutasVifVfor = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
];
//metodo - methods
const handleClick = (message) => {
  console.log(message);
  // console.log('Me diste click');
}

const counterA = ref(0)

const incrementA = () => {
  // console.log('Aumentar contador');
  counterA.value++
  console.log(counterA)
}

const decrementA = () => {
  // console.log('Aumentar contador');
  counterA.value--
  console.log(counterA)
}

const resetA = () => {
  counterA.value = 0
  console.log(counterA)
}

const colorMayorA = 'color:green'
const colorMenorA = 'color:red'

const counterB = ref(0)
const addList = ref([])

const incrementB = () => {
  // console.log('Aumentar contador');
  counterB.value++
  // console.log(counterB)
}

const decrementB = () => {
  // console.log('Aumentar contador');
  counterB.value--
  // console.log(counterB)
}

const resetB = () => {
  counterB.value = 0
  // console.log(counterB)
}

const colorMayorB = 'color:green'
const colorMenorB = 'color:red'

const classCounter = computed(() => {
  // Recibe en su interior una función de flecha y siempre retorna algo, es una propiedad computada, es algo que va a estar realizando un computo, pero Ojo: siempre tiene que existir un return
  if (counterB.value === 0)
    return 'colorZeroB'
  if (counterB.value > 0) {
    return 'colorMayorB'
  }
  if (counterB.value < 0) {
    return 'colorMenorB'
  }
})

const add = () => {
  addList.value.push(counterB.value)
}

const bloquearBtnAdd = computed(() => {
  const numSearch = addList.value.find(num => num === counterB.value)
  console.log(numSearch);
  if (numSearch === 0) return true
  return numSearch ? true : false
})


</script>


<style>
h1 {
  color: aqua
}

.colorMayorA {
  color: green;
}

.colorMenorA {
  color: red;
}

.colorMayorB {
  color: green;
}

.colorMenorB {
  color: red;
}

.colorZeroB {
  color: blue;
}
</style>