<script setup lang="ts">
import type { Post } from "../types/Post";
import NoComments from "./NoComments.vue";
import PostLoader from "./PostLoader.vue";

const props = defineProps<{
  post: Post;
  deleting: number | null;
}>();

const emit = defineEmits<{
  edit: [post: Post];
  delete: [post: Post];
}>();
</script>

<template>
  <PostLoader v-if="deleting && deleting === props.post.id"></PostLoader>
  <div v-else class="block">
    <div class="is-flex is-justify-content-space-between is-align-items-center">
      <h2 class="title">
        #{{ props.post.id }}: {{ props.post.title }}
      </h2>
      <div class="is-flex">
        <span
          class="icon is-small is-right is-clickable"
          @click="$emit('edit', props.post)"
        >
          <i class="fas fa-pen-to-square"></i>
        </span>
        <span
          class="icon is-small is-right has-text-danger is-clickable ml-3"
          @click="$emit('delete', props.post)"
        >
          <i class="fas fa-trash"></i>
        </span>
      </div>
    </div>
    <div class="block">
      <p data-cy="PostBody">{{ props.post.body }}</p>
    </div>

    <NoComments></NoComments>
  </div>
</template>
