<template>
  <div class="space-y-3">
    <!-- Summary Stats -->
    <div class="grid grid-cols-3 gap-3 mb-4">
      <div class="bg-red-50 border border-red-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-red-700">{{ criticalVulns }}</div>
        <div class="text-sm text-red-600">Critical</div>
      </div>
      <div class="bg-orange-50 border border-orange-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-orange-700">{{ highVulns }}</div>
        <div class="text-sm text-orange-600">High</div>
      </div>
      <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3 text-center">
        <div class="text-2xl font-bold text-yellow-700">{{ totalVulns }}</div>
        <div class="text-sm text-yellow-600">Total</div>
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

    <!-- Vulnerabilities List -->
    <div class="space-y-2 max-h-80 overflow-y-auto">
      <div
        v-for="vuln in filteredVulnerabilities"
        :key="`${vuln.vulnerability}-${vuln.library}`"
        class="border rounded-lg p-3 hover:bg-gray-50 transition"
        :class="getVulnerabilityBorderColor(vuln.severity)"
      >
        <div class="flex justify-between items-start">
          <div class="flex-1">
            <div class="flex items-center gap-2 mb-2">
              <h4 class="font-semibold text-slate-800">{{ vuln.library }}</h4>
              <UiChip :class="getSeverityColor(vuln.severity)" outline>
                <i class="mdi mdi-shield-alert"></i>
                {{ vuln.severity.toUpperCase() }}
              </UiChip>
            </div>
            
            <div class="space-y-1 text-sm">
              <div class="flex items-center gap-2">
                <span class="text-slate-600">CVE:</span>
                <code class="bg-gray-100 px-2 py-1 rounded text-xs">{{ vuln.vulnerability }}</code>
              </div>
              <div class="flex items-center gap-2">
                <span class="text-slate-600">Version:</span>
                <span class="font-mono">{{ vuln.version }}</span>
              </div>
              <div class="flex items-center gap-2">
                <span class="text-slate-600">Project:</span>
                <span>{{ vuln.project }}</span>
              </div>
              <div class="mt-2">
                <p class="text-slate-700">{{ vuln.description }}</p>
              </div>
            </div>
          </div>
          
          <div class="flex flex-col gap-2 ml-4">
            <button
              @click="viewVulnerability(vuln)"
              class="px-3 py-1 text-sm bg-blue-100 text-blue-700 rounded hover:bg-blue-200 transition"
              title="View Details"
            >
              <i class="mdi mdi-eye"></i>
            </button>
            <button
              @click="fixVulnerability(vuln)"
              class="px-3 py-1 text-sm bg-green-100 text-green-700 rounded hover:bg-green-200 transition"
              title="Fix Now"
            >
              <i class="mdi mdi-wrench"></i>
            </button>
            <button
              @click="dismissVulnerability(vuln)"
              class="px-3 py-1 text-sm bg-gray-100 text-gray-700 rounded hover:bg-gray-200 transition"
              title="Dismiss"
            >
              <i class="mdi mdi-close"></i>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Empty State -->
    <div v-if="filteredVulnerabilities.length === 0" class="text-center py-8 text-slate-600">
      <i class="mdi mdi-shield-check text-4xl mb-2 text-green-500"></i>
      <p>No vulnerabilities found!</p>
      <p class="text-sm">Your libraries are secure.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Vulnerability {
  library: string
  version: string
  vulnerability: string
  severity: 'critical' | 'high' | 'medium' | 'low'
  project: string
  description: string
}

const props = defineProps<{
  vulnerabilities: Vulnerability[]
}>()

const severityFilter = ref('all')
const projectFilter = ref('all')

const filteredVulnerabilities = computed(() => {
  return props.vulnerabilities.filter(vuln => {
    const matchesSeverity = severityFilter.value === 'all' || vuln.severity === severityFilter.value
    const matchesProject = projectFilter.value === 'all' || vuln.project === projectFilter.value
    return matchesSeverity && matchesProject
  })
})

const totalVulns = computed(() => props.vulnerabilities.length)

const criticalVulns = computed(() => 
  props.vulnerabilities.filter(vuln => vuln.severity === 'critical').length
)

const highVulns = computed(() => 
  props.vulnerabilities.filter(vuln => vuln.severity === 'high').length
)

const getSeverityColor = (severity: string) => {
  switch (severity) {
    case 'critical':
      return 'text-red-800 border-red-400 bg-red-50'
    case 'high':
      return 'text-orange-800 border-orange-400 bg-orange-50'
    case 'medium':
      return 'text-yellow-800 border-yellow-400 bg-yellow-50'
    case 'low':
      return 'text-blue-800 border-blue-400 bg-blue-50'
    default:
      return 'text-gray-800 border-gray-400 bg-gray-50'
  }
}

const getVulnerabilityBorderColor = (severity: string) => {
  switch (severity) {
    case 'critical':
      return 'border-l-4 border-l-red-500'
    case 'high':
      return 'border-l-4 border-l-orange-500'
    case 'medium':
      return 'border-l-4 border-l-yellow-500'
    case 'low':
      return 'border-l-4 border-l-blue-500'
    default:
      return 'border-l-4 border-l-gray-500'
  }
}

const viewVulnerability = (vuln: Vulnerability) => {
  console.log('Viewing vulnerability:', vuln.vulnerability)
  // Implementation for viewing vulnerability details
}

const fixVulnerability = (vuln: Vulnerability) => {
  console.log('Fixing vulnerability:', vuln.vulnerability)
  // Implementation for fixing vulnerability
}

const dismissVulnerability = (vuln: Vulnerability) => {
  console.log('Dismissing vulnerability:', vuln.vulnerability)
  // Implementation for dismissing vulnerability
}
</script>