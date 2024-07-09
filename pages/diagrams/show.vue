<template>
  <div class="flex h-full">
    <div class="w-3/4 bg-slate-50">
      <ClientOnly fallback-tag="span" fallback="Loading diagram...">
        <LazyDiagramsDiagram />
      </ClientOnly>
    </div>
    <div class="w-1/4 bg-slate-100 p-2 overflow-y-auto">
      <DiagramsCard />
      <UiCard>
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCreate />
      </UiCard>
    </div>
  </div>
</template>
<script setup lang="ts">

</script>
