<template>
  <LazyUiCard class="mb-3">
    <div class="flex justify-between items-center">
      <div>
        <NuxtLink to="/ethical/show" class="block">
          <h3 class="text-lg font-bold text-slate-800 transition hover:text-rose-900">
            <i class="mdi mdi-cctv"></i>
            NNFF: Saldos y Movimientos
          </h3>
        </NuxtLink>
        <UsersChip />
        <p class="text-slate-600 text-sm mb-1">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam nec purus nec nunc tincidunt ultricies. Nullam nec purus nec nunc tincidunt ultricies.</p>
        <UiChip class="me-2" outline>
          <i class="mdi mdi-application-settings-outline me-1"></i>
          3 components
        </UiChip>
        <UiChip class="me-2" outline>
          <i class="mdi mdi-comment-text-multiple-outline me-1"></i>
          5 Comments
        </UiChip>
      </div>
      <div class="border-s ps-3 min-w-[250px]">
        <p class="text-sm text-slate-600">
          Created at: <time datetime="2021-09-01">September 1, 2021</time> <br>
          Updated at: <time datetime="2021-09-01">September 2, 2021</time> <br>
          By: <a href="#" class="text-rose-900">John Doe</a><br>
          Provider: <span class="text-blue-600">Droni.co | DevSec</span><br>
          Status: <span class="text-green-600">Open</span>
        </p>
      </div>
    </div>
    <div class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700 mt-2">
      <div class="bg-green-600 h-2.5 rounded-full dark:bg-green-500" :style="`width: ${Math.floor(Math.random() * 100)}%`"></div>
    </div>
  </LazyUiCard>
</template>
<script setup lang="ts">
</script>