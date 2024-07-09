<template>
  <UiCard class="mb-2">
    <!-- crete comment -->
    <div>
      <textarea
        v-model="comment"
        class="w-full p-2 border rounded focus:outline-none focus:ring focus:border-rose-500 text-slate-600"
        placeholder="Write a comment..."
      ></textarea>
    </div>
    <div class="text-end">
      <button
        @click="createComment"
        class="p-2 bg-rose-900 text-rose-100 hover:bg-rose-800 transition rounded-lg"
      >
        <i class="mdi mdi-send"></i>
        Send
      </button>
    </div>
  </UiCard>
</template>
<script setup lang="ts">
const comment = ref('')
const createComment = () => {
  console.log(comment.value)
}
</script>