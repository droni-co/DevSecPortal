<template>
  <VueFlow :nodes="nodes" :edges="edges" />
</template>
<script setup lang="ts">
import type { Node, Edge } from '@vue-flow/core'
import { VueFlow } from '@vue-flow/core'
import '@vue-flow/core/dist/style.css'
import '@vue-flow/core/dist/theme-default.css'
const nodes: Node[] = [
{
    id: '1',
    type: 'input',
    position: { x: 350, y: 105 },
    // all nodes can have a data object containing any data you want to pass to the node
    // a label can property can be used for default nodes
    data: { label: 'Component AppiService NNFF 00-325' },
  },
  {
    id: '2',
    position: { x: 200, y: 300 },
    data: { label: 'NNFF Front-Consulta-EEFF' },
  },
  {
    id: '3',
    position: { x: 550, y: 400 },
    data: { label: 'Frontdor' },
  },
  {
    id: '4',
    position: { x: 450, y: 500 },
    data: { label: 'Apim Externo' },
  },
  {
    id: '5',
    position: { x: 250, y: 600 },
    data: { label: 'DB: Transaccional' },
  }
]

const edges: Edge[] = [
  {
    id: 'e1->2',
    source: '1',
    target: '2',
  },
  {
    id: 'e1->3',
    source: '1',
    target: '3',
    animated: true,
  },
  {
    id: 'e2->5',
    source: '2',
    target: '5',
    animated: true,
  },
  {
    id: 'e3->4',
    source: '3',
    target: '4',

  },
]
</script>