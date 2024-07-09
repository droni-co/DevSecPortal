<template>
  <div class="container mx-auto">
    <UiTitle title="Dashboard" />
    <div class="flex mb-3">
      <div class="w-1/3 px-2">
        <ClientOnly fallback-tag="span" fallback="Loading diagram...">
          <DashboardFirstChart />
        </ClientOnly>
      </div>
      <div class="w-2/3 px-2">
        <ClientOnly fallback-tag="span" fallback="Loading diagram...">
          <DashboardSecondChart />
        </ClientOnly>
      </div>
    </div>
    <div class="flex">
      <div class="w-1/2 px-2">
        <UiCard>
          <UiTitle title="Ethical Hacking" level="h4" />
          <EthicalRow />
          <EthicalRow />
        </UiCard>
      </div>
      <div class="w-1/2 px-2">
        <UiCard>
          <UiTitle title="Security cases" level="h4" />
          <SecurityRow />
          <SecurityRow />
        </UiCard>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
</script>