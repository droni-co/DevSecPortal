<template>
  <UiCard>
    <h2 class="text-xl flex">
      <i class="mdi mdi-application-settings-outline me-2"></i>
      NegociosFiduciarios-Front-Consulta-EEFF
    </h2>
    <p class="text-sm text-slate-600 mb-2">Lorem ipsum dolor sit amet consectetur adipisicing elit. Fuga, praesentium! Aperiam corrupti blanditiis cumque adipisci dignissimos quis vero iusto sequi eaque! Nostrum suscipit hic quam sapiente nulla! Ratione, nihil! Quibusdam?</p>
    <UiChip class="me-2">
      <i class="mdi mdi-github me-1"></i>
      Repository
    </UiChip>

    <a href="#">
      <UiChip class="me-2" clickable>
        <i class="mdi mdi-rocket-launch-outline me-1"></i>
        Pipeline
      </UiChip>
    </a>
    <a href="#">
      <UiChip class="me-2" outline clickable>
        <i class="mdi mdi-comment-text-multiple-outline me-1"></i>
        5 Comments
      </UiChip>
    </a>
    <NuxtLink to="/swagger">
      <UiChip clickable>
        <i class="mdi mdi-code-block-braces"></i>
        Swagger Tester
      </UiChip>
    </NuxtLink>
  </UiCard>
</template>
<script setup lang="ts">


</script>