<template>
  <div class="flex h-full">
    <div class="w-1/5 bg-slate-100 p-2 overflow-y-auto">
      <UiTitle title="Diagrams">
        <nuxt-link to="/" class="p-2 bg-slate-900 text-slate-100 hover:bg-slate-800 transition rounded-lg">
          <i class="mdi mdi-plus"></i> Add diagram
        </nuxt-link>
      </UiTitle>
      <input
        type="search"
        class="w-full p-2 border rounded focus:outline-none focus:ring focus:border-rose-500 text-slate-600"
        placeholder="Search diagram..."
        />
      <DiagramsCard class="mb-2 cursor-pointer" />
      <DiagramsCard class="mb-2" />
      <DiagramsCard class="mb-2" />
      <DiagramsCard class="mb-2" />
      <DiagramsCard class="mb-2" />
    </div>
    <div class="w-4/5 bg-slate-800">
      
    </div>
  </div>
</template>
<script setup lang="ts">

</script>
