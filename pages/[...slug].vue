<script setup lang="ts">
const route = useRoute()

const { data: page } = await useAsyncData(() => {
  return queryContent().where({ _path: route.path }).findOne()
})
</script>

<template>
  <div class="prose mx-auto p-4">
    <ContentRenderer v-if="page" :value="page" />
    <p v-else class="text-red-500">Content not found: {{ route.path }}</p>
  </div>
</template>