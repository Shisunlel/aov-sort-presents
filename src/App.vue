<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center">
        <img
          v-for="present in sortedPresents"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <button
        @click="isSorted = !isSorted"
        class="mt-4 flex mx-auto focus:outline-none focus:ring-2 focus:ring-emerald-600 focus:ring-offset-2 focus:ring-offset-emerald-50 bg-green hover:bg-emerald-600 text-white rounded-lg py-3 px-6"
      >
        Toggle sort
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import presents from './presents.json'
const isSorted = ref(false)
const clonedPresent = [...presents]
clonedPresent.sort((a, b) => {
  const areaA = a.dimensions.width * a.dimensions.height
  const areaB = b.dimensions.width * b.dimensions.height
  if (areaA < areaB) return -1
  if (areaA > areaB) return 1
  return 0
})
const sortedPresents = computed(() => {
  if (!isSorted.value) return presents
  return clonedPresent
})
</script>
