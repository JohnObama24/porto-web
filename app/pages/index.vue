<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => {
  return queryCollection('index').first()
})
if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page not found',
    fatal: true
  })
}

useSeoMeta({
  title: page.value?.seo.title || page.value?.title,
  ogTitle: page.value?.seo.title || page.value?.title,
  description: page.value?.seo.description || page.value?.description,
  ogDescription: page.value?.seo.description || page.value?.description
})
</script>

<template>
  <UPage v-if="page">
    <LandingHero :page />
    <UPageSection :ui="{ container: '!pt-0 flex flex-col lg:flex-row gap-8' }">
      <div class="flex-1  p-4 rounded-xl">
        <LandingAbout :page="page" />
      </div>

      <div class="flex-1 flex flex-col gap-4">
        <div class=" p-4 rounded-xl">
          <LandingWorkExperience :page="page" />
        </div>
        <div class=" p-4 rounded-xl">
          <LandingEducationExperience :page="page" />
        </div>
      </div>
    </UPageSection>
    <LandingBlog :page />
    <LandingTestimonials :page />
    <LandingFAQ :page />
  </UPage>
</template>
