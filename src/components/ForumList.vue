<script setup>

const props = defineProps({
  forums: { type: Array, required: true },
  title: { type: String, default: 'Forums' },
  categoryId: { type: String, required: false}
})

function forumThreadsWord(forum) {
  if (forum.threads?.length) {
    return forum.threads.length > 1 ? 'threads' : 'thread'
  } else {
    return 'No threads'
  }
}

</script>

<template>
  <div class="col-full">
    <div class="forum-list">
      <h2 class="list-title">
        <RouterLink v-if="categoryId" :to="{name: 'Category', params: {id: categoryId}}">{{ title }}</RouterLink>
        <span v-else>{{ title }}</span>
      </h2>

      <div class="forum-listing" v-for="forum in props.forums" :key="forum.id">
        <div class="forum-details">
          <RouterLink class="text-xlarge" :to="{name: 'Forum', params: {id: forum.id}}">
            {{ forum.name }}
          </RouterLink>
          <p>{{ forum.description }}</p>
        </div>

        <div class="threads-count">
          <p>
          <span class="count">
            {{ forum.threads?.length }}
          </span>
            {{ forumThreadsWord(forum) }}
          </p>
        </div>

        <div class="last-thread">

        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
