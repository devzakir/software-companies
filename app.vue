<template>
  <div class="min-h-full">
    <app-header />
    <main>
      <div class="max-w-7xl mx-auto py-4 sm:px-6 lg:px-8">
        <div class="my-4">
          <div class="py-24 text-center rounded-md bg-green-500">
            <h2 class="text-4xl mb-4"> Top software companies in Dhaka </h2>
            <p class="text-lg"> Find the top software companies in dhaka, browse by category to narrow your search. </p>
          </div>
        </div>
        <div class="flex gap-5">
          <div class="w-5/12">
            <label for="" class="text-xs uppercase text-gray-400">Enter name</label>
            <input type="text" class="py-3 outline-none px-6 bg-gray-100 rounded-md text-base w-full my-1 focus:ring-1 ring-green-500" placeholder="Enter company name">
          </div>
          <div class="w-4/12">
            <category-dropdown />
          </div>
          <div class="w-3/12">
            <select-list />
          </div>
        </div>
        <div class="pt-4 grid gap-4 grid-cols-3">
          <company-item :item="item" v-for="(item, index) in data" :key="index" />
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import SelectList from './components/global/SelectList.vue'
const { data } = await useAsyncData('companies', () => queryContent('/companies').find())
</script>
