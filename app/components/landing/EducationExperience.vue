<script setup lang="ts">
import type { IndexCollectionItem } from '@nuxt/content'

defineProps<{
  page: IndexCollectionItem
}>()
</script>

<template>
  <UPageSection
    :title="page.education.title"
    :ui="{
      container: '!p-0 gap-4 sm:gap-4',
      title: 'text-left text-xl sm:text-xl lg:text-2xl font-medium',
      description: 'mt-2'
    }"
  >
    <template #description>
      <div class="flex flex-col gap-2">
        <Motion
          v-for="(edu, index) in page.education.items"
          :key="index"
          :initial="{ opacity: 0, transform: 'translateY(20px)' }"
          :while-in-view="{ opacity: 1, transform: 'translateY(0)' }"
          :transition="{ delay: 0.4 + 0.2 * index }"
          :in-view-options="{ once: true }"
          class="text-muted flex items-center text-nowrap gap-2"
        >
          <p class="text-sm">
            {{ edu.date }}
          </p>
          <USeparator />
          <ULink
            class="flex items-center gap-1"
            :to="edu.school.url"
            target="_blank"
          >
            <span class="text-sm">
              {{ edu.degree }}
            </span>
            <div
              class="inline-flex items-center gap-1"
              :style="{ color: edu.school.color }"
            >
              <span class="font-medium">{{ edu.school.name }}</span>
              <UIcon :name="edu.school.logo" />
            </div>
          </ULink>
        </Motion>
      </div>
    </template>
  </UPageSection>
</template>
