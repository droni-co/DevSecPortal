<template>
  <div class="flex flex-col h-full">
    <div class="p-3">
      <div class="flex">
        <select v-model="fetchModel.method" class="p-2 mb-2">
          <option value="GET">GET</option>
          <option value="POST">POST</option>
          <option value="PUT">PUT</option>
          <option value="DELETE">DELETE</option>
        </select>
        <input v-model="fetchModel.endpoint" class="p-2 mb-2 grow" placeholder="Endpoint" />
      </div>
      
      
      <table class="table-auto w-full mb-2">
        <thead>
          <tr>
            <th class="border px-4 py-2">Key</th>
            <th class="border px-4 py-2">Value</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(_value, key) in fetchModel.headers" :key="key">
            <td class="border px-4 py-2">{{ key }}</td>
            <td class="border px-4 py-2">
              <input v-model="fetchModel.headers[key]" class="w-full" />
            </td>
          </tr>
        </tbody>
      </table>
      <textarea v-model="fetchModel.body" class="w-full p-2 mb-2" placeholder="Body" />
      <button @click="testFetch" class="w-full p-2 bg-blue-500 text-white">
        Test endpoint
      </button>
    </div>
    <div class="bg-gray-800 text-gray-100 h-full overflow-auto">
      <span class="relative flex h-3 w-3" v-if="loading">
        <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-sky-400 opacity-75"></span>
        <span class="relative inline-flex rounded-full h-3 w-3 bg-sky-500"></span> Loading
      </span>
      <pre><code>{{ fetchModel.response }}</code></pre>
    </div>
    
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
const fetchModel = ref({
  endpoint: 'https://azfd-qa-lab-sss-001.azurefd.net/portalptc-v2-experiencia/get/mutual-funds/account-sif',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6ImpBNkxtalFoc1RCa1lJZld0NUpsSDgxeDVlTXlBQUNjYjhTUFJ4a1NlRTAiLCJ0eXAiOiJKV1QifQ.eyJhdWQiOiI0ZjU1Nzc2My1kYjNlLTQ4MzgtYjczMi0xNWJmMTkwNjdhMzEiLCJpc3MiOiJodHRwczovL3FhbGFiY2FwaXRhbGIyYy5iMmNsb2dpbi5jb20vYzRhNDEwZjYtY2VhOS00ZmQxLWFjNWQtMGMyMjlkZDEyZTY2L3YyLjAvIiwiZXhwIjoxNzIwMDU0NjMzLCJuYmYiOjE3MjAwNTM3MzMsInN1YiI6IjljOGRkNzY5LThlZWItNGYyNS1iZjAzLTc5MjhiZWEwOTgzYyIsInNpZ25Jbk5hbWUiOiIxMDMzNjUxODU1IiwidGlkIjoiYzRhNDEwZjYtY2VhOS00ZmQxLWFjNWQtMGMyMjlkZDEyZTY2IiwidGZwIjoiQjJDXzFBX1RyYW5zYWNjaW9uYWxfc2lnbmluIiwibm9uY2UiOiI2MzQ3M2UzOS03MzUxLTRkZGMtYmZjNC03M2ZlYTI2NDUzMTIiLCJhenAiOiI0ZjU1Nzc2My1kYjNlLTQ4MzgtYjczMi0xNWJmMTkwNjdhMzEiLCJ2ZXIiOiIxLjAiLCJpYXQiOjE3MjAwNTM3MzN9.DNrMvW2vkpAFQdmD3mbbBmTy_13pPfJWyG-jeqAd0c587mESJaSYJ4VBe8iUNUvhAsPpBfVfDpslDT_g8Lvdozf_y117_5MJHSKkvuGddUO5SRHZ5snMsg-vIPmAbTJWhBzZoHT-aFNxNNyklXvxdYNPTR1OsmtbM-TmF_bSTh6ry5FPTOSvKm9PqtvuZL1ODcnh_-gUDLEKNSjUFJkfLakFE_MhRioZki3g-y5ZB5vZVvNw7pusgEmpnnJF8yD7NvB1Kdu0W153juFEM_UhR6ZEgofJ_41Koskw1zEIVF3dsD8l9MjlOIauMHF1GUZ91jLS1JN30dTobD3CNSXXpA'
  },
  body: '{ "noDocument": "800167643" }',
  response: { data: 'No data' }
} as {
  endpoint: string;
  method: string;
  headers: { [key: string]: string };
  body: string;
  response: any;
})
const newHeaderKey = ref('')
const loading = ref(false)

const fullResponse = ref(null as any)

const testFetch = async () => {
  console.log('testFetch')
  loading.value = true
  fetch(fetchModel.value.endpoint, {
    method: fetchModel.value.method,
    headers: fetchModel.value.headers,
    body: fetchModel.value.body.length > 0 ? fetchModel.value.body : null
  }).then(async (response) => {
    fullResponse.value = response
    fetchModel.value.response = await response.json()
  }).catch((error) => {
    console.error(error)
    fetchModel.value.response = error.code
  }).finally(() => {
    loading.value = false
  })
}
</script>