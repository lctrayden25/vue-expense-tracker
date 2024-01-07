<template>
  <h4>Your Balance</h4>
  <h1 id="balance" class="font-bold text-2xl">${{ total }}</h1>
</template>

<script lang="ts" setup>
import { toRefs, watchEffect } from 'vue'
const props = defineProps({
  total: {
    type: Number,
    required: true
  }
})

const { total } = toRefs(props)

watchEffect(() => {
  console.log(total.value)
})

</script>
