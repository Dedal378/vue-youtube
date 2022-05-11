<script setup>
import { computed, ref } from 'vue'
import TheSearchInput from './TheSearchInput.vue'
import TheSearchButton from './TheSearchButton.vue'
import TheSearchResults from './TheSearchResults.vue'

const query = ref('')
const keywords = ref([
  'new york giants',
  'new york alicia keys',
  'new york giants vs washington football',
  'new york',
  'new york songs',
  'new york new york frank sinatra',
  'new york jets',
  'new york city',
  'new york giants live',
  'new york sate of mind',
  'new york giants vs washington football live',
  'new york giants injury',
  'new york giants live stream',
  'new york accent',
])

const results = computed(() => keywords.value.filter((result) => result.includes(query.value)))
</script>

<template>
  <div class="flex w-full mr-2">
    <div class="relative flex w-full">
      <TheSearchInput v-model:query.no-spaces="query" />
      <TheSearchResults
        v-show="query"
        :results="results"
      />
    </div>

    <TheSearchButton />
  </div>
</template>
