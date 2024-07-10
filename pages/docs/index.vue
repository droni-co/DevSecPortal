<template>
  <div class="flex h-full">
    <div class="w-1/4 px-3 overflow-auto">
      <UiCollapse title="Backend Good Practices" class="mb-3" group="parent">
        <ul>
          <li v-for="path in ExampleSwagger.paths" :key="path">
            <button @click="openPath = path" class="block w-full p-2 text-left bg-slate-900 text-slate-100 transition hover:bg-slate-400">
              {{ path?.post?.summary ?? path?.get?.summary }}
            </button>
          </li>
        </ul>
      </UiCollapse>
      <UiCollapse title="Frontend documentation" class="mb-3" group="parent">
        <ul>
          <li v-for="path in ExampleSwagger.paths" :key="path">
            <button @click="openPath = path" class="block w-full p-2 text-left bg-slate-900 text-slate-100 transition hover:bg-slate-400">
              {{ path?.post?.summary ?? path?.get?.summary }}
            </button>
          </li>
        </ul>
      </UiCollapse>
      <UiCollapse title="Security" class="mb-3" group="parent">
        <ul>
          <li v-for="path in ExampleSwagger.paths" :key="path">
            <button @click="openPath = path" class="block w-full p-2 text-left bg-slate-900 text-slate-100 transition hover:bg-slate-400">
              {{ path?.post?.summary ?? path?.get?.summary }}
            </button>
          </li>
        </ul>
      </UiCollapse>
      <UiCollapse title="DevOps" class="mb-3" group="parent">
        <ul>
          <li v-for="path in ExampleSwagger.paths" :key="path">
            <button @click="openPath = path" class="block w-full p-2 text-left bg-slate-900 text-slate-100 transition hover:bg-slate-400">
              {{ path?.post?.summary ?? path?.get?.summary }}
            </button>
          </li>
        </ul>
      </UiCollapse>
    </div>
    <div class="flex flex-col h-full w-3/4 border">
      <div class="flex items-center justify-between px-2 bg-slate-800 text-slate-100 w-100">
        <h1 class="text-lg grow">Document to edit</h1>
        <button class="p-2 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="view" @click="view = !view">
          <i class="mdi mdi-eye-outline"></i>
          View / Edit
        </button>
        <button class="p-2 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Save">
          <i class="mdi mdi-content-save-outline"></i>
          Save
        </button>
      </div>
      <div v-if="view" class="grow w-full bg-white block p-3 overflow-auto">
        <article class="prose" v-html="markdown.render(String(response))"></article>
      </div>
      <MonacoEditor v-else v-model="response" lang="markdown" :options="{ theme: 'vs-dark',  wordWrap: 'on', tabSize: 2 }" class="grow w-full" />
    </div>
  </div>
</template>
<script setup lang="ts">
import MarkdownIt from "markdown-it";
const markdown = new MarkdownIt();
import ExampleSwagger from '../../data/exampleSwagger.json'
const openPath = ref('[get]/ping')
const view = ref(true)
const response = ref(`# Hola mundo
Este es un ejemplo de un documento markdown
## Subtitulo
Este es un subtitulo
- Lista
- de
- elementos
# Hola mundo
Este es un ejemplo de un documento markdown
## Subtitulo
Este es un subtitulo
- Lista
- de
- elementos
# Hola mundo
Este es un ejemplo de un documento markdown
## Subtitulo
Este es un subtitulo
- Lista
- de
- elementos
# Hola mundo
Este es un ejemplo de un documento markdown
## Subtitulo
Este es un subtitulo
- Lista
- de
- elementos
`)

</script>
