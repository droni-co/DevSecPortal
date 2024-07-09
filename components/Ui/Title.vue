<template>
  <header class="flex p-2 border-b mb-3">
    <div class="grow">
      <h1 class="font-bold text-2xl text-slate-800">
        {{ props.title }}
      </h1>
    </div>
    <div class="pt-1">
      <slot />
    </div>
  </header>
</template>
<script setup lang="ts">
const props = defineProps({
  title: {
    type: String,
    required: true
  }
})
</script>