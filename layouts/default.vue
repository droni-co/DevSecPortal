<template>
  <div class="flex h-screen">
    <LazyMainMenu />
    <div class="grow bg-slate-100 h-screen flex flex-col">
      <LazyMainHeader />
      <main class="flex-grow overflow-y-auto">
        <slot />
      </main>
    </div>
  </div>
</template>