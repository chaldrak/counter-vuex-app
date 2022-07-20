<template>
  <h1>Vuex counter</h1>
  <h1 class="counter">{{ counter }}</h1>
  <button @click="substractToCounter(value)">-</button>
  <input 
    type="number" 
    v-model="value"
  />
  <button @click="addToCounter(value)">+</button>
  <div>
    <button class="btn" @click="addRandomNumber">
      Add by Random Number
      <!-- <img style="width: 15px;" v-if="loading" src="https://i.imgur.com/JfPpwOA.gif" alt="" /> -->
    </button>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
import { useStore } from 'vuex'

const value = ref(1)

const loading = ref(false)

const store = useStore()

const counter = computed(() => {
  return store.state.counter
})

function addToCounter(params) {
  return store.commit("addToCounter", params)
}

function substractToCounter(params) {
  return store.commit("substractToCounter", params)
}

function addRandomNumber(params) {
  loading.value = true
  store.dispatch("addRandomNumber", params)
    .then(loading.value = false)
  console.log(loading.value)
}

</script>

<style>
.counter {
  font-size: 5rem;
}
button {
  border-radius: 100%;
  border: none;
  width: 2rem;
  height: 2rem;
  font-weight: 700;
  cursor: pointer;
}
input {
  padding: 0.4rem;
  margin: 0 0.5rem;
  text-align: center;
}
.btn {
  border-radius: 0.5rem;
  width: auto;
  background-color: #41B983;
  margin-top: 1rem;
  color: white;
}
</style>