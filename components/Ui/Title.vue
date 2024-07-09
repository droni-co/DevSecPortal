<template>
  <header class="flex p-2 border-b mb-3">
    <div class="grow">
      <h1
        class="font-bold text-slate-800"
        :class="{ 'text-2xl': props.level === 'h1', ' text-xl': props.level === 'h2', 'text-lg': props.level === 'h3', 'text-base': props.level === 'h4' }"
        >
        <i v-if="props.icon" :class="props.icon"></i>
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
  },
  icon: {
    type: String,
    default: ''
  },
  name: {
    type: String,
    default: ''
  },
  level: {
    type: String,
    default: 'h1'
  }
})
</script>