<template>
  <div class="flex h-full">
    <div class="w-3/4 px-3 overflow-auto pt-2">
      <EthicalRow />
      <hr class="my-3">
      <UiCard class="mb-3">
        <UiTitle icon="mdi mdi-toy-brick-outline" title="Components" level="h3" />
        <div class="grid grid-cols-3 gap-3">
          <ComponentsCard />
          <ComponentsCard />
          <ComponentsCard />
        </div>
      </UiCard>

      <UiCard class="mb-3">
        <UiTitle icon="mdi mdi-sitemap-outline" title="Diagrams" level="h3" />
        <div class="grid grid-cols-4 gap-4">
          <NuxtLink to="/diagrams/show" class="cursor-pointer">
            <DiagramsCard />
          </NuxtLink>
          <NuxtLink to="/diagrams/show" class="cursor-pointer">
            <DiagramsCard />
          </NuxtLink>
        </div>
      </UiCard>
    </div>
    <div class="w-1/4 bg-slate-200 overflow-auto">
      <div class="flex">
        <UiFormButton class="grow" @click="activeTab = 'comments'" :class="{ 'border-b-4 border-rose-400': activeTab === 'comments' }">
          <i class="mdi mdi-comment-text-multiple-outline me-1"></i>
          5 Comments
        </UiFormButton>
        <UiFormButton class="grow" @click="activeTab = 'checklist'" :class="{ 'border-b-4 border-rose-400': activeTab === 'checklist' }">
          <i class="mdi mdi-shield-check-outline"></i>
          CheckList
        </UiFormButton>
      </div>
      <UiCard v-if="activeTab === 'comments'">
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCreate />
      </UiCard>
      <EthicalChecklist v-if="activeTab === 'checklist'" />
    </div>
  </div>
</template>
<script setup lang="ts">
const activeTab = ref('comments')
</script>