<template>
  <div class="container">
    <h4>History</h4>
    <div class="flex">
      <p
        v-for="(number, index) in history"
        :key="index"
        :class="activeIndexes(value).includes(index) && 'bold'"
      >
        {{ number }}
      </p>
    </div>
    <input 
      type="number"
      placeholder="search by index"
      v-model="value"
    >
  </div>
</template>

<script setup>
import { computed, ref } from '@vue/runtime-core'
import { useStore } from 'vuex'

const store = useStore()

const value = ref()

const history = computed(() => {
  return store.state.history
})

const activeIndexes = computed(() => {
  return store.getters.activeIndexes
})

</script>

<style>
.container {
  margin-top: 7rem;
}
.flex {
  display: flex;
  text-align: center;
  width: 25rem;
  margin: 0 auto;
  justify-content: center;
  flex-wrap: wrap;
}
.flex p {
  margin: 1rem;
}
.bold {
  font-weight: 900;
  color: #41B390;
}
</style>