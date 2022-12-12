<template>
  <div class="top-16 w-full">
    <label for="category" class="text-xs uppercase text-gray-400">Select Category</label>
    <Combobox v-model="selected">
      <div class="relative mt-1">
        <div
          class="relative w-full cursor-default overflow-hidden rounded-lg bg-white text-left focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-green-300 sm:text-sm">
          <!-- <ComboboxInput id="category"
            class="w-full border-none py-3 pl-3 pr-10 text-base leading-5 bg-gray-100 text-gray-900 focus:ring-0"
            :displayValue="(person) => person.name" @change="query = $event.target.value" /> -->
          <ComboboxButton class="absolute inset-y-0 right-0 flex items-center pr-2">
            <SelectorIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
          </ComboboxButton>
        </div>
        <TransitionRoot leave="transition ease-in duration-100" leaveFrom="opacity-100" leaveTo="opacity-0"
          @after-leave="query = ''">
          <ComboboxOptions
            class="absolute mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm">
            <div v-if="filteredPeople.length === 0 && query !== ''"
              class="relative cursor-default select-none py-2 px-4 text-gray-700">
              Nothing found.
            </div>

            <ComboboxOption v-for="person in filteredPeople" as="template" :key="person.id" :value="person"
              v-slot="{ selected, active }">
              <li class="relative cursor-default select-none py-2 pl-10 pr-4" :class="{
                  'bg-green-600 text-white': active,
                  'text-gray-900': !active,
                }">
                <span class="block truncate" :class="{ 'font-medium': selected, 'font-normal': !selected }">
                  {{ person.name }}
                </span>
                <span v-if="selected" class="absolute inset-y-0 left-0 flex items-center pl-3"
                  :class="{ 'text-white': active, 'text-green-600': !active }">
                  <CheckIcon class="h-5 w-5" aria-hidden="true" />
                </span>
              </li>
            </ComboboxOption>
          </ComboboxOptions>
        </TransitionRoot>
      </div>
    </Combobox>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import {
  Combobox,
  ComboboxInput,
  ComboboxButton,
  ComboboxOptions,
  ComboboxOption,
  TransitionRoot,
} from '@headlessui/vue'
import { CheckIcon, SelectorIcon } from '@heroicons/vue/solid'

const people = [
  { id: 1, name: 'Software Agency' },
  { id: 2, name: 'Shopify' },
  { id: 3, name: 'WordPress' },
  { id: 4, name: 'Game Development' },
  { id: 5, name: 'Mobile Apps' },
  { id: 6, name: 'ML & AI' },
  { id: 7, name: 'Desktop' },
  { id: 8, name: 'SAAS' },
  { id: 8, name: 'IOT' },
  { id: 8, name: 'Blockchain' },
]

let selected = ref(people[0])
let query = ref('')

let filteredPeople = computed(() =>
  query.value === ''
    ? people
    : people.filter((person) =>
        person.name
          .toLowerCase()
          .replace(/\s+/g, '')
          .includes(query.value.toLowerCase().replace(/\s+/g, ''))
      )
)
</script>
