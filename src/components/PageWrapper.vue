<script lang="ts" setup>
defineProps(['heading'])
</script>

<template>
  <div class="relative flex items-center justify-center w-full">
    <div class="max-w-xl w-full mx-auto p-5 bg-slate-200 h-full m-5">
      <h1>{{ heading }}</h1>
    </div>
  </div>
</template>
