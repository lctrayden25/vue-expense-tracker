<template>
  <div class="shadow-lg bg-white flex justify-between p-3 mt-5">
    <div class="w-[50%] text-center">
      <h4>Income</h4>
      <p class="text-green-500">{{ income }}</p>
    </div>
    <div class="w-[50%] text-center">
      <h4>Expense</h4>
      <p class="text-red-500">{{ expense }}</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { toRefs } from 'vue'

const props = defineProps({
  income: {
    type: String
    // required: true
  },
  expense: {
    type: String
    // required: true
  }
})

const { income, expense } = toRefs(props)
</script>
