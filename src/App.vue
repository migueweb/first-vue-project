<script setup>
import { ref, computed } from 'vue';

let counter = ref(0)

const increment = () => counter.value++

const decrement = () => counter.value--

const reset = () => counter.value = 0

/* Favorites */
let favorites = ref([])

const add = () => favorites.value.push(counter.value)

const blockAddBtn = computed(() => {

  let found = favorites.value.find(number => number === counter.value)

  return found || found === 0

})

const classCounter = computed(() => {
  if(counter.value === 0 ) return 'bg-secondary'
  
  return counter.value > 0 ? 'bg-success' : 'bg-danger'
})
</script>


<template>
  <div class="container text-center">

    <h2 :class="classCounter" class="counter border border-dark border-3 mx-auto">{{ counter }}</h2>

    <!-- START BUTTONS -->
    <button @click="increment" class="btn btn-light border border-3 ms-2">Increment</button>

    <button @click="decrement" class="btn btn-light border border-3 ms-2">Decrement</button>

    <button @click="reset" class="btn btn-light border border-3 ms-2">Reset</button>

    <button @click="add" :disabled="blockAddBtn" class="btn btn-primary border border-3 ms-2">Add to favorites</button>
    <!-- END BUTTONS -->

    <h2 class="ms-2 mt-4">Favorites</h2>

    <div class="mx-auto col-3">
      <ul class="list-group">
        <li v-for="(item, index) of favorites" :key="index" class="list-group-item"> {{ item }}</li>
      </ul>
    </div>

  </div>
</template>

<style>
.counter {
  padding: 1rem 1.5rem;
  width: fit-content;
  margin: 1rem;
}
</style>