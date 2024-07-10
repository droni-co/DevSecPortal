<template>
  <MonacoEditor v-model="value" lang="typescript" />
</template>
<script lang="ts" setup>
const value = ref('')
</script>