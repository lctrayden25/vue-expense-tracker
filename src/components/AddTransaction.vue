<template>
  <div>
    <h3 class="font-normal w-full border-b border-b-slate-400 py-2">Add new transaction</h3>
    <form class="py-2 flex flex-col gap-4" @submit.prevent="onFormSubmit">
      <div class="flex flex-col gap-2">
        <label for="text">Expense</label>
        <input
          type="text"
          id="text"
          v-model="expense"
          placeholder="Enter text..."
          class="px-4 py-1"
        />
      </div>
      <div class="flex flex-col gap-2">
        <label for="amount">Amount</label>
        <input
          type="number"
          id="amount"
          v-model="amount"
          placeholder="Enter amount..."
          class="px-4 py-1"
        />
      </div>
      <button class="w-full bg-black p-2 text-white">Add transction</button>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

export type FormDataType = {
  expense: string
  amount: number | null
}

const expense = ref('')
const amount = ref(null)

const emit = defineEmits(['transactionSubmitted'])

const onFormSubmit = () => {
  const transactionData = {
    expense: expense.value,
    amount: amount.value
  }

  emit('transactionSubmitted', transactionData)

  amount.value = null
  expense.value = ''
}
</script>
