<template>
  <div class="flex h-full">
    <div class="w-1/2 px-3 overflow-auto">
      <ComponentsCard class="mb-3" />
      <div v-for="path, urlIndex in ExampleSwagger.paths ?? []" class="border-b bg-white p-2 hover:bg-slate-200">
        <UiChip outline>{{ urlIndex }}</UiChip>
        <div class="cursor-pointer hover:bg-slate-300" v-for="mehtod, methodIndex in path" @click="openPath = `[${methodIndex}]${urlIndex}`">
          <UiChip>{{ String(methodIndex).toUpperCase() }}</UiChip>
          {{ (mehtod as any)?.summary }}
          <div v-if="openPath === `[${methodIndex}]${urlIndex}`" class="border rounded p-2">
            <div class="py-2">
              <UiChip outline v-for="param in (mehtod as any)?.parameters ?? []">
                {{ param.name }} "{{ param.in }}"              
              </UiChip>
            </div>
            <UiFormButton outline size="s" @click="response = { data: urlIndex + ' Unauthorized' }">
              <i class="mdi mdi-invoice-send-outline"></i>
              Test endpoint
            </UiFormButton>
            <UiFormButton outline size="s" @click="response = path">
              <i class="mdi mdi-file-document-outline"></i>
              View docs
            </UiFormButton>
          </div>
        </div>
      </div>
    </div>
    <div class="w-1/2 p-3 bg-slate-900 overflow-auto text-white break-words">
      <code>{{ JSON.stringify(response) }}</code>
    </div>
  </div>
</template>
<script setup lang="ts">
import ExampleSwagger from '../../data/exampleSwagger.json'
const openPath = ref('[get]/ping')
const response = ref({})

</script>
