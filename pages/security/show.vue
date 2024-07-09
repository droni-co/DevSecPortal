<template>
  <div class="flex h-full">
    <div class="w-3/5 px-3 overflow-auto">
      <UiTitle icon="mdi mdi-bug-pause-outline" title="Case test 123 Cross Site request forgering">
        <UiFormSelect
          class="min-w-[10rem]"
          v-model="status"
          :options="[
            { id: 1, name: 'Open' },
            { id: 2, name: 'Closed' },
            { id: 3, name: 'In Progress' }
          ]"
        />
      </UiTitle>
      <UiCard>

        <UsersChip /> <UsersChip />
        <p class="text-sm text-slate-600">
          Created at: <time datetime="2021-09-01">September 1, 2021</time> |
          Updated at: <time datetime="2021-09-01">September 2, 2021</time> <br>

          Level: <span class="text-blue-600">High</span> |
          Status: <span class="text-green-600">Open</span>
        </p>
        <p class="text-slate-600 text-sm mb-1">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam nec purus nec nunc tincidunt ultricies. Nullam nec purus nec nunc tincidunt ultricies.
        </p>
        <UiChip class="me-2" outline>
          <i class="mdi mdi-application-settings-outline me-1"></i>
          NegociosFiduciarios-Front-Consulta-EEFF
        </UiChip>
        <UiChip class="me-2" outline>
          <i class="mdi mdi-comment-text-multiple-outline me-1"></i>
          5 Comments
        </UiChip>
      </UiCard>
      <hr class="my-3">
      <UiCard>
        <img src="https://www.slideteam.net/wp/wp-content/uploads/2023/02/SI4.jpg" alt="Report" class="h-48 rounded-lg shadow-lg mb-3" />
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam nec purus nec nunc tincidunt ultricies. Nullam nec purus nec nunc tincidunt ultricies. Lorem ipsum dolor sit amet consectetur adipisicing elit. Beatae quas enim at incidunt aliquid obcaecati, ratione nostrum iste minima? Unde, doloribus quis! Veritatis nostrum repudiandae velit quas atque, iusto neque! Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum qui tenetur dolore quam aliquid perspiciatis similique libero delectus reprehenderit, praesentium saepe et rem fuga quis pariatur deserunt minus corporis quasi.
        </p>
      </UiCard>
    </div>
    <div class="w-2/5 bg-slate-200 overflow-auto">
      <div class="flex">
        <UiFormButton class="grow" @click="activeTab = 'comments'" :class="{ 'border-b-4 border-rose-400': activeTab === 'comments' }">
          <i class="mdi mdi-comment-text-multiple-outline me-1"></i>
          5 Comments
        </UiFormButton>
        <UiFormButton class="grow" @click="activeTab = 'test'" :class="{ 'border-b-4 border-rose-400': activeTab === 'test' }">
          <i class="mdi mdi-play-network-outline"></i>
          Test report
        </UiFormButton>
      </div>
      <UiCard v-if="activeTab === 'comments'">
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCard />
        <CommentsCreate />
      </UiCard>
      <SecurityTest v-if="activeTab === 'test'" />
    </div>
  </div>
</template>
<script setup lang="ts">
const activeTab = ref('comments')
const status = ref(3)
</script>