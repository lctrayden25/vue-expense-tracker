<template>
  <div class="my-6">
    <h3 class="font-normal w-full border-b border-b-slate-400 py-2">History</h3>
    <ul class="py-2 flex flex-col gap-2">
      <li
        class="flex justify-between border-r-4 gap-3 items-center group"
        v-for="transaction in transactions"
        v-bind:key="transaction.id"
      >
        <button
          class="group-hover:flex w-[15px] h-[15px] hidden bg-red-500 items-center justify-center text-sm text-white"
          @click="onDelete(transaction.id)"
        >
          x
        </button>
        <div
          class="bg-white p-2 shadow-md flex items-center justify-between w-full border-r-4"
          :class="
            transaction.amount !== null && transaction?.amount < 0
              ? 'border-r-red-500'
              : 'border-r-green-500'
          "
        >
          {{ transaction.expense }} <span>{{ transaction.amount }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts"></script>

<script lang="ts" setup>
import { toRefs } from 'vue'
import type { PropType } from 'vue'

export type TransactionType = {
  id: number
  expense: string
  amount: number
}[]

const props = defineProps({
  transactions: {
    type: Array as PropType<TransactionType>,
    required: true
  }
})

const { transactions } = toRefs(props)

const emit = defineEmits(['transactionDelete'])

const onDelete = (id: any) => {
  emit('transactionDelete', id)
}
</script>
