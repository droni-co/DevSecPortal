<template>
  <div class="container mx-auto">
    <UiTitle title="Security Cases">
      <nuxt-link to="/" class="p-2 bg-slate-900 text-slate-100 hover:bg-slate-800 transition rounded-lg">
        <i class="mdi mdi-plus"></i> New security case
      </nuxt-link>
    </UiTitle>

    <input
      type="search"
      class="w-full p-2 border rounded focus:outline-none focus:ring focus:border-rose-500 text-slate-600 mb-4"
      placeholder="Search security case..."
      />

    <SecurityRow />
    <SecurityRow />
    <SecurityRow />
    <SecurityRow />
  </div>
</template>
<script setup lang="ts">
</script>