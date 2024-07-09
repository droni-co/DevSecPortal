<template>
  <div class="container mx-auto">
      <UiTitle title="Diagrams">
        <nuxt-link to="/" class="p-2 bg-slate-900 text-slate-100 hover:bg-slate-800 transition rounded-lg">
          <i class="mdi mdi-plus"></i> Add diagram
        </nuxt-link>
      </UiTitle>
      <input
        type="search"
        class="w-full p-2 border rounded focus:outline-none focus:ring focus:border-rose-500 text-slate-600 mb-4"
        placeholder="Search diagram..."
        />
      <div class="grid grid-cols-4 gap-4">
        <NuxtLink to="/diagrams/show" class="cursor-pointer">
          <DiagramsCard />
        </NuxtLink>
        <NuxtLink to="/diagrams/show" class="cursor-pointer">
          <DiagramsCard />
        </NuxtLink>
        <NuxtLink to="/diagrams/show" class="cursor-pointer">
          <DiagramsCard />
        </NuxtLink>
        <NuxtLink to="/diagrams/show" class="cursor-pointer">
          <DiagramsCard />
        </NuxtLink>
        <NuxtLink to="/diagrams/show" class="cursor-pointer">
          <DiagramsCard />
        </NuxtLink>
      </div>
    </div>
</template>
<script setup lang="ts">


</script>
