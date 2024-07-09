<template>
  <div class="flex h-screen">
    <LazyMainMenu />
    <main class="flex-1 bg-slate-100">
      <slot />
    </main>
  </div>
</template>