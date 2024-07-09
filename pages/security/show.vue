<template>
  <div class="flex h-full">
    <div class="w-3/5">
      <UiTitle title="Case test 123 Cross Site request forgering" />
      <LazyUiTable :headers="[
        { label: 'id', name: 'id' },
      ]" :data="[]" />
    </div>
    <div class="w-2/5 bg-teal-100">
      Detalle
    </div>
  </div>
</template>
<script setup lang="ts">
</script>