// TODO: Fix slugPath logic to correctly display markdown blog posts

<script setup lang="ts">
import { useRoute } from "vue-router";
import { queryContent } from "#content";

const route = useRoute();

// Join slug to form full path (e.g. hello-world → /blog/hello-world)
const slugPath = Array.isArray(route.params.slug)
  ? `/blog/${route.params.slug.join("/")}`
  : `/blog/${route.params.slug}`;

console.log("Slug Path:", slugPath); // helpful for debugging

const { data: post } = await useAsyncData(() =>
  queryContent().where({ _path: slugPath }).findOne()
);
</script>

<template>
  <div class="prose mx-auto p-8">
    <ContentRenderer v-if="post" :value="post" />
    <p v-else class="text-red-500">Post not found at: {{ slugPath }}</p>
  </div>
</template>
