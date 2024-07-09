<template>
  <div class="whitespace-nowrap rounded-lg  py-1 px-3 border font-sans text-xs inline-block"
    :class="{
      'text-slate-900 bg-slate-100 border-slate-900': props.outline,
      'text-white bg-slate-900': !props.outline,
      'transition hover:text-white hover:bg-slate-900': clickable && props.outline,
      'transition hover:text-slate-900 hover:bg-slate-100': clickable && !props.outline
    }"
    >
    <slot />
  </div>
</template>
<script lang="ts" setup>
const props = defineProps({
  outline: {
    type: Boolean,
    default: false
  },
  clickable: {
    type: Boolean,
    default: false
  }
})
</script>