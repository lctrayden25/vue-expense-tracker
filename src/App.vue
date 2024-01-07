<template>
  <div class="relative w-full p-8">
    <div class="max-w-xl w-full h-full bg-slate-100 mx-auto py-5 px-10">
      <Header />
      <Balance :total="Number(total)" />
      <IncomeExpense :income="income" :expense="expense" />
      <TransactionList
        :transactions="transactions"
        :onTransactionDelete="handleTransactionDelete"
      />
      <AddTransaction @transactionSubmitted="handleTransactionSubmit" />
      <ul>
        <li
          v-for="transaction in transactions"
          v-bind:key="transaction.id"
          @click="handleTransactionDelete(transaction.id)"
        >
          {{ transaction.expense }}
        </li>
      </ul>
      <div>total: {{ total }} income: {{ income }} expense: {{ expense }}</div>
    </div>
    </div>
  <!-- <RouterView></RouterView> -->
</template>

<script lang="ts" setup>
// import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList, { type TransactionType } from './components/TransactionList.vue'
import AddTransaction, { type FormDataType } from './components/AddTransaction.vue'

import { computed, ref } from 'vue'

// export default {
//   components: {
//     Header,
//     Balance,
//     IncomeExpense,
//     TransactionList,
//     AddTransaction
//   } as any
// }

let transactions = ref([
  { id: 1, expense: 'Flower', amount: 169.9 },
  { id: 2, expense: 'Flower', amount: -29.9 },
  { id: 3, expense: 'Flower', amount: -39.9 }
] as TransactionType)

const total = computed(() => {
  return transactions?.value
    ?.reduce((acc, transaction) => {
      return acc + transaction?.amount
    }, 0)
    .toFixed(2)
})

let income = computed(() => {
  return transactions?.value
    ?.filter((t) => t?.amount > 0)
    ?.reduce((acc, transaction) => {
      return acc + transaction?.amount
    }, 0)
    .toFixed(2)
})

const expense = computed(() => {
  return transactions?.value
    ?.filter((t) => t?.amount < 0)
    ?.reduce((acc, transactions) => {
      return acc + transactions?.amount
    }, 0)
    .toFixed(2)
})

const handleTransactionSubmit = (transactionData: FormDataType) => {
  transactions.value?.push({
    id: generateRandomId(),
    expense: transactionData.expense,
    amount: transactionData.amount || 0
  })
}

const handleTransactionDelete = (id: number) => {
  transactions.value = transactions.value?.filter((transaction) => transaction?.id !== id)
}

const generateRandomId = () => {
  return Math.floor(Math.random() * 1000000)
}
</script>
