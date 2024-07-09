<template>
  <div class="container mx-auto">
    <UiTitle title="Components">
      <nuxt-link to="/" class="p-2 bg-slate-900 text-slate-100 hover:bg-slate-800 transition rounded-lg">
        <i class="mdi mdi-plus"></i> Register Component
      </nuxt-link>
    </UiTitle>
    <p class="text-slate-700 mb-3">Lorem ipsum dolor sit amet consectetur adipisicing elit. Ducimus saepe cupiditate pariatur doloribus? Voluptatem earum amet cum, vero quisquam corporis laudantium in vitae consequatur officiis dolorem, iure assumenda distinctio. Labore?</p>
    <input
      type="search"
      class="w-full p-2 border rounded focus:outline-none focus:ring focus:border-rose-500 text-slate-600 mb-4"
      placeholder="Search component..."
      />
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <ComponentsCard />
      <ComponentsCard />
      <ComponentsCard />
      <ComponentsCard />
    </div>
  </div>
</template>
<script setup lang="ts">

</script>
