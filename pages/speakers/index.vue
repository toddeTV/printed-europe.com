<script setup lang="ts">
const route = useRoute()

const { data: speakers } = await useAsyncData(route.path, () => queryCollection('speakers').all())

const title = 'Speakers List'
const description = 'List of speakers for the event'

useSeoMeta({
  title,
  ogTitle: title,

  description,
  ogDescription: description,
})
</script>

<template>
  <template v-if="speakers">
    <AppHeader :description="description" :title="title" />

    <div v-for="speaker in speakers" :key="speaker.slug">
      <NuxtLink :to="`/speakers/${speaker.slug}`">
        {{ speaker.name }}
      </NuxtLink>
    </div>
  </template>
</template>
