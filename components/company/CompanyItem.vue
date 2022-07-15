<template>
  <div class="border border-gray-300 p-4 rounded-lg">
    <h3 class="text-3xl mb-2">{{ item.name }}</h3>
    <p class="mb-2 text-gray-500 text-sm">{{ item.description }}</p>
    <div class="flex gap-2">
      <label v-if="item.type" class="rounded-full text-xs capitalize px-4 py-1 bg-green-200 text-gray-800">{{ item.type }}</label>
      <a :href="item.url" :target="_blank" v-if="item.url" class="flex decoration-none px-4 py-1 rounded-full border text-gray-600 border-gray-200 text-xs">Visit <ExternalLinkIcon class="ml-1 h-4 w-4" /> </a>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['item'])

import { ExternalLinkIcon } from '@heroicons/vue/outline'
</script>

<style>

</style>
