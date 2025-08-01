<template>
  <div class="container mx-auto">
    <UiTitle title="Library Tracking Dashboard" icon="mdi mdi-package-variant">
      <button class="p-2 bg-slate-900 text-slate-100 hover:bg-slate-800 transition rounded-lg">
        <i class="mdi mdi-plus"></i> Add Project
      </button>
    </UiTitle>

    <!-- Search Section -->
    <UiCard class="mb-4">
      <UiTitle title="Library Search" level="h3" />
      <LibrariesSearch @search="handleSearch" />
    </UiCard>

    <!-- Reports Section -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-4 mb-4">
      <!-- Outdated Libraries Panel -->
      <UiCard>
        <UiTitle title="Outdated Libraries" level="h3" icon="mdi mdi-clock-alert-outline" />
        <LibrariesOutdatedPanel :libraries="outdatedLibraries" />
      </UiCard>

      <!-- Vulnerabilities Panel -->
      <UiCard>
        <UiTitle title="Security Vulnerabilities" level="h3" icon="mdi mdi-shield-alert-outline" />
        <LibrariesVulnerabilitiesPanel :vulnerabilities="vulnerabilities" />
      </UiCard>
    </div>

    <!-- Projects Overview -->
    <UiCard>
      <UiTitle title="Projects Overview" level="h3" />
      <LibrariesProjectsList :projects="projects" />
    </UiCard>
  </div>
</template>

<script setup lang="ts">
// Mock data for demonstration
const outdatedLibraries = ref([
  {
    name: 'lodash',
    current: '4.17.15',
    latest: '4.17.21',
    project: 'Frontend Portal',
    severity: 'medium'
  },
  {
    name: 'axios',
    current: '0.21.1',
    latest: '1.6.2',
    project: 'API Gateway',
    severity: 'high'
  },
  {
    name: 'express',
    current: '4.17.1',
    latest: '4.18.2',
    project: 'Backend Services',
    severity: 'low'
  }
])

const vulnerabilities = ref([
  {
    library: 'lodash',
    version: '4.17.15',
    vulnerability: 'CVE-2021-23337',
    severity: 'high',
    project: 'Frontend Portal',
    description: 'Command injection vulnerability'
  },
  {
    library: 'node-fetch',
    version: '2.6.1',
    vulnerability: 'CVE-2022-0235',
    severity: 'critical',
    project: 'API Gateway',
    description: 'Information exposure vulnerability'
  }
])

const projects = ref([
  {
    name: 'Frontend Portal',
    libraries: 45,
    outdated: 12,
    vulnerabilities: 3,
    lastScan: '2024-01-15'
  },
  {
    name: 'API Gateway',
    libraries: 32,
    outdated: 8,
    vulnerabilities: 1,
    lastScan: '2024-01-14'
  },
  {
    name: 'Backend Services',
    libraries: 28,
    outdated: 5,
    vulnerabilities: 0,
    lastScan: '2024-01-13'
  }
])

const handleSearch = (searchTerm: string) => {
  console.log('Searching for:', searchTerm)
  // Implement search functionality
}
</script>