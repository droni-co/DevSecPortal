<template>
  <div class="space-y-3">
    <!-- Summary Stats -->
    <div class="grid grid-cols-3 gap-3 mb-4">
      <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-yellow-700">{{ totalOutdated }}</div>
        <div class="text-sm text-yellow-600">Total Outdated</div>
      </div>
      <div class="bg-orange-50 border border-orange-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-orange-700">{{ highPriority }}</div>
        <div class="text-sm text-orange-600">High Priority</div>
      </div>
      <div class="bg-red-50 border border-red-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-red-700">{{ criticalUpdates }}</div>
        <div class="text-sm text-red-600">Critical</div>
      </div>
    </div>

    <!-- Filter and Sort -->
    <div class="flex gap-2 mb-4">
      <select
        v-model="severityFilter"
        class="px-3 py-1 border rounded text-sm focus:outline-none focus:ring-2 focus:border-blue-500"
      >
        <option value="all">All Severities</option>
        <option value="critical">Critical</option>
        <option value="high">High</option>
        <option value="medium">Medium</option>
        <option value="low">Low</option>
      </select>
      <select
        v-model="projectFilter"
        class="px-3 py-1 border rounded text-sm focus:outline-none focus:ring-2 focus:border-blue-500"
      >
        <option value="all">All Projects</option>
        <option value="Frontend Portal">Frontend Portal</option>
        <option value="API Gateway">API Gateway</option>
        <option value="Backend Services">Backend Services</option>
      </select>
    </div>

    <!-- Outdated Libraries List -->
    <div class="space-y-2 max-h-80 overflow-y-auto">
      <div
        v-for="library in filteredLibraries"
        :key="`${library.name}-${library.project}`"
        class="border rounded-lg p-3 hover:bg-gray-50 transition"
      >
        <div class="flex justify-between items-start">
          <div class="flex-1">
            <div class="flex items-center gap-2">
              <h4 class="font-semibold text-slate-800">{{ library.name }}</h4>
              <UiChip :class="getSeverityColor(library.severity)" outline>
                {{ library.severity }}
              </UiChip>
            </div>
            <p class="text-sm text-slate-600 mb-2">{{ library.project }}</p>
            <div class="flex gap-2 text-sm">
              <span class="text-red-600">
                <i class="mdi mdi-arrow-down-circle"></i>
                Current: {{ library.current }}
              </span>
              <span class="text-green-600">
                <i class="mdi mdi-arrow-up-circle"></i>
                Latest: {{ library.latest }}
              </span>
            </div>
          </div>
          <div class="flex gap-2">
            <button
              @click="viewDetails(library)"
              class="px-3 py-1 text-sm bg-blue-100 text-blue-700 rounded hover:bg-blue-200 transition"
              title="View Details"
            >
              <i class="mdi mdi-information"></i>
            </button>
            <button
              @click="updateLibrary(library)"
              class="px-3 py-1 text-sm bg-green-100 text-green-700 rounded hover:bg-green-200 transition"
              title="Update"
            >
              <i class="mdi mdi-update"></i>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Empty State -->
    <div v-if="filteredLibraries.length === 0" class="text-center py-8 text-slate-600">
      <i class="mdi mdi-check-circle text-4xl mb-2 text-green-500"></i>
      <p>No outdated libraries found!</p>
      <p class="text-sm">All libraries are up to date.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface OutdatedLibrary {
  name: string
  current: string
  latest: string
  project: string
  severity: 'critical' | 'high' | 'medium' | 'low'
}

const props = defineProps<{
  libraries: OutdatedLibrary[]
}>()

const severityFilter = ref('all')
const projectFilter = ref('all')

const filteredLibraries = computed(() => {
  return props.libraries.filter(lib => {
    const matchesSeverity = severityFilter.value === 'all' || lib.severity === severityFilter.value
    const matchesProject = projectFilter.value === 'all' || lib.project === projectFilter.value
    return matchesSeverity && matchesProject
  })
})

const totalOutdated = computed(() => props.libraries.length)

const highPriority = computed(() => 
  props.libraries.filter(lib => lib.severity === 'high' || lib.severity === 'critical').length
)

const criticalUpdates = computed(() => 
  props.libraries.filter(lib => lib.severity === 'critical').length
)

const getSeverityColor = (severity: string) => {
  switch (severity) {
    case 'critical':
      return 'text-red-700 border-red-300'
    case 'high':
      return 'text-orange-700 border-orange-300'
    case 'medium':
      return 'text-yellow-700 border-yellow-300'
    case 'low':
      return 'text-blue-700 border-blue-300'
    default:
      return 'text-gray-700 border-gray-300'
  }
}

const viewDetails = (library: OutdatedLibrary) => {
  console.log('Viewing details for:', library.name)
  // Implementation for viewing library details
}

const updateLibrary = (library: OutdatedLibrary) => {
  console.log('Updating library:', library.name)
  // Implementation for updating library
}
</script>