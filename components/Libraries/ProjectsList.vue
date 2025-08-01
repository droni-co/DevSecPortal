<template>
  <div class="space-y-4">
    <!-- Projects Table -->
    <div class="overflow-x-auto">
      <table class="w-full border-collapse border border-gray-200">
        <thead>
          <tr class="bg-gray-50">
            <th class="border border-gray-200 px-4 py-3 text-left text-sm font-semibold text-gray-700">
              Project Name
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Total Libraries
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Outdated
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Vulnerabilities
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Last Scan
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Health Score
            </th>
            <th class="border border-gray-200 px-4 py-3 text-center text-sm font-semibold text-gray-700">
              Actions
            </th>
          </tr>
        </thead>
        <tbody>
          <tr 
            v-for="project in projects" 
            :key="project.name"
            class="hover:bg-gray-50 transition"
          >
            <td class="border border-gray-200 px-4 py-3">
              <div class="flex items-center gap-2">
                <i class="mdi mdi-folder-outline text-blue-600"></i>
                <span class="font-medium text-slate-800">{{ project.name }}</span>
              </div>
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center">
              <span class="font-mono text-sm">{{ project.libraries }}</span>
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center">
              <UiChip 
                :class="project.outdated > 0 ? 'bg-yellow-100 text-yellow-800' : 'bg-green-100 text-green-800'"
              >
                {{ project.outdated }}
              </UiChip>
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center">
              <UiChip 
                :class="getVulnerabilityColor(project.vulnerabilities)"
              >
                {{ project.vulnerabilities }}
              </UiChip>
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center text-sm text-slate-600">
              {{ formatDate(project.lastScan) }}
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center">
              <div class="flex items-center justify-center gap-2">
                <div class="w-16 bg-gray-200 rounded-full h-2">
                  <div 
                    class="h-2 rounded-full transition-all duration-300"
                    :class="getHealthScoreColor(getHealthScore(project))"
                    :style="{ width: `${getHealthScore(project)}%` }"
                  ></div>
                </div>
                <span class="text-sm font-medium" :class="getHealthScoreTextColor(getHealthScore(project))">
                  {{ getHealthScore(project) }}%
                </span>
              </div>
            </td>
            <td class="border border-gray-200 px-4 py-3 text-center">
              <div class="flex justify-center gap-1">
                <button
                  @click="scanProject(project)"
                  class="px-2 py-1 text-xs bg-blue-100 text-blue-700 rounded hover:bg-blue-200 transition"
                  title="Scan Now"
                >
                  <i class="mdi mdi-radar"></i>
                </button>
                <button
                  @click="viewProject(project)"
                  class="px-2 py-1 text-xs bg-gray-100 text-gray-700 rounded hover:bg-gray-200 transition"
                  title="View Details"
                >
                  <i class="mdi mdi-eye"></i>
                </button>
                <button
                  @click="updateProject(project)"
                  class="px-2 py-1 text-xs bg-green-100 text-green-700 rounded hover:bg-green-200 transition"
                  title="Update All"
                >
                  <i class="mdi mdi-update"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Summary Cards -->
    <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mt-6">
      <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 text-center">
        <div class="text-2xl font-bold text-blue-700">{{ totalProjects }}</div>
        <div class="text-sm text-blue-600">Total Projects</div>
      </div>
      <div class="bg-green-50 border border-green-200 rounded-lg p-4 text-center">
        <div class="text-2xl font-bold text-green-700">{{ totalLibraries }}</div>
        <div class="text-sm text-green-600">Total Libraries</div>
      </div>
      <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4 text-center">
        <div class="text-2xl font-bold text-yellow-700">{{ totalOutdated }}</div>
        <div class="text-sm text-yellow-600">Outdated Libraries</div>
      </div>
      <div class="bg-red-50 border border-red-200 rounded-lg p-4 text-center">
        <div class="text-2xl font-bold text-red-700">{{ totalVulnerabilities }}</div>
        <div class="text-sm text-red-600">Vulnerabilities</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Project {
  name: string
  libraries: number
  outdated: number
  vulnerabilities: number
  lastScan: string
}

const props = defineProps<{
  projects: Project[]
}>()

const totalProjects = computed(() => props.projects.length)
const totalLibraries = computed(() => props.projects.reduce((sum, p) => sum + p.libraries, 0))
const totalOutdated = computed(() => props.projects.reduce((sum, p) => sum + p.outdated, 0))
const totalVulnerabilities = computed(() => props.projects.reduce((sum, p) => sum + p.vulnerabilities, 0))

const getHealthScore = (project: Project) => {
  const total = project.libraries
  const issues = project.outdated + (project.vulnerabilities * 2) // Weight vulnerabilities more
  const score = Math.max(0, Math.round(((total - issues) / total) * 100))
  return score
}

const getHealthScoreColor = (score: number) => {
  if (score >= 80) return 'bg-green-500'
  if (score >= 60) return 'bg-yellow-500'
  if (score >= 40) return 'bg-orange-500'
  return 'bg-red-500'
}

const getHealthScoreTextColor = (score: number) => {
  if (score >= 80) return 'text-green-700'
  if (score >= 60) return 'text-yellow-700'
  if (score >= 40) return 'text-orange-700'
  return 'text-red-700'
}

const getVulnerabilityColor = (count: number) => {
  if (count === 0) return 'bg-green-100 text-green-800'
  if (count <= 2) return 'bg-yellow-100 text-yellow-800'
  return 'bg-red-100 text-red-800'
}

const formatDate = (dateString: string) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'short', 
    day: 'numeric' 
  })
}

const scanProject = (project: Project) => {
  console.log('Scanning project:', project.name)
  // Implementation for scanning project
}

const viewProject = (project: Project) => {
  console.log('Viewing project:', project.name)
  // Implementation for viewing project details
}

const updateProject = (project: Project) => {
  console.log('Updating project:', project.name)
  // Implementation for updating project libraries
}
</script>