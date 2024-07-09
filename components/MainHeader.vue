<template>
  <header class="bg-slate-800 text-white flex">
    <UiFormInput v-model="search" placeholder="Search..." />
    <UiFormButton>Search</UiFormButton>
    <UiFormButton>Logout</UiFormButton>
  </header>
</template>
<script setup lang="ts">
import { ref } from 'vue'
const search = ref('')
</script>
