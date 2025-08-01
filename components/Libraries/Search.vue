<template>
  <div class="space-y-4">
    <!-- Search Form -->
    <div class="flex gap-3">
      <div class="flex-1">
        <input
          v-model="searchTerm"
          type="search"
          class="w-full p-3 border rounded-lg focus:outline-none focus:ring-2 focus:border-blue-500 text-slate-600"
          placeholder="Search for npm packages (e.g., lodash, axios, express)..."
          @keyup.enter="performSearch"
        />
      </div>
      <select
        v-model="searchFilter"
        class="p-3 border rounded-lg focus:outline-none focus:ring-2 focus:border-blue-500 text-slate-600"
      >
        <option value="all">All Projects</option>
        <option value="frontend">Frontend Portal</option>
        <option value="api">API Gateway</option>
        <option value="backend">Backend Services</option>
      </select>
      <button
        @click="performSearch"
        class="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition"
      >
        <i class="mdi mdi-magnify"></i> Search
      </button>
    </div>

    <!-- Search Results -->
    <div v-if="searchResults.length > 0" class="mt-4">
      <UiTitle title="Search Results" level="h4" />
      <div class="space-y-2">
        <div
          v-for="result in searchResults"
          :key="result.name"
          class="p-3 border rounded-lg bg-gray-50 hover:bg-gray-100 transition"
        >
          <div class="flex justify-between items-start">
            <div>
              <h4 class="font-semibold text-slate-800">{{ result.name }}</h4>
              <p class="text-sm text-slate-600">{{ result.description }}</p>
              <div class="flex gap-2 mt-2">
                <UiChip outline>Current: {{ result.currentVersion }}</UiChip>
                <UiChip outline>Latest: {{ result.latestVersion }}</UiChip>
                <UiChip :class="getProjectColor(result.project)" outline>
                  {{ result.project }}
                </UiChip>
              </div>
            </div>
            <div class="text-right">
              <span
                :class="getStatusColor(result.status)"
                class="text-sm font-medium px-2 py-1 rounded"
              >
                {{ result.status }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- No Results -->
    <div v-else-if="hasSearched" class="text-center py-8 text-slate-600">
      <i class="mdi mdi-magnify text-4xl mb-2"></i>
      <p>No libraries found matching your search criteria.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface SearchResult {
  name: string
  description: string
  currentVersion: string
  latestVersion: string
  project: string
  status: 'up-to-date' | 'outdated' | 'vulnerable'
}

const emit = defineEmits<{
  search: [searchTerm: string]
}>()

const searchTerm = ref('')
const searchFilter = ref('all')
const searchResults = ref<SearchResult[]>([])
const hasSearched = ref(false)

// Mock search data
const mockLibraries: SearchResult[] = [
  {
    name: 'lodash',
    description: 'A modern JavaScript utility library delivering modularity, performance & extras.',
    currentVersion: '4.17.15',
    latestVersion: '4.17.21',
    project: 'Frontend Portal',
    status: 'vulnerable'
  },
  {
    name: 'axios',
    description: 'Promise based HTTP client for the browser and node.js',
    currentVersion: '0.21.1',
    latestVersion: '1.6.2',
    project: 'API Gateway',
    status: 'outdated'
  },
  {
    name: 'express',
    description: 'Fast, unopinionated, minimalist web framework for node.js',
    currentVersion: '4.17.1',
    latestVersion: '4.18.2',
    project: 'Backend Services',
    status: 'outdated'
  },
  {
    name: 'vue',
    description: 'The progressive JavaScript framework',
    currentVersion: '3.3.8',
    latestVersion: '3.3.8',
    project: 'Frontend Portal',
    status: 'up-to-date'
  },
  {
    name: 'typescript',
    description: 'TypeScript is a language for application-scale JavaScript',
    currentVersion: '5.0.2',
    latestVersion: '5.3.3',
    project: 'All Projects',
    status: 'outdated'
  }
]

const performSearch = () => {
  hasSearched.value = true
  emit('search', searchTerm.value)
  
  // Filter results based on search term and project filter
  searchResults.value = mockLibraries.filter(lib => {
    const matchesSearch = !searchTerm.value || 
      lib.name.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      lib.description.toLowerCase().includes(searchTerm.value.toLowerCase())
    
    const matchesFilter = searchFilter.value === 'all' || 
      lib.project.toLowerCase().includes(searchFilter.value)
    
    return matchesSearch && matchesFilter
  })
}

const getStatusColor = (status: string) => {
  switch (status) {
    case 'up-to-date':
      return 'bg-green-100 text-green-800'
    case 'outdated':
      return 'bg-yellow-100 text-yellow-800'
    case 'vulnerable':
      return 'bg-red-100 text-red-800'
    default:
      return 'bg-gray-100 text-gray-800'
  }
}

const getProjectColor = (project: string) => {
  const colors = [
    'text-blue-600',
    'text-green-600',
    'text-purple-600',
    'text-orange-600'
  ]
  return colors[project.length % colors.length]
}
</script>