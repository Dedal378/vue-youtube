<script setup>
import { computed, inject, ref, watch } from 'vue'
import TheSearchInput from './TheSearchInput.vue'
import TheSearchButton from './TheSearchButton.vue'
import TheSearchResults from './TheSearchResults.vue'

const emits = defineEmits(['update-search-query'])
const { searchQuery } = inject('searchQuery')
const query = ref(searchQuery)
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
const isSearchResultsShown = ref(false)

const trimmedQuery = () => query.value.replace(/\s+/g, ' ').trim()
const results = computed(() => {
  if (!query.value) {
    return []
  }

  return keywords.value.filter((result) => result.includes(trimmedQuery()))
})
const toggleSearchResults = (isSearchInputActive) => {
  isSearchResultsShown.value = isSearchInputActive && results.value.length
}

watch(query, (query) => {
  emits('update-search-query', query)
})
</script>

<template>
  <div class="flex w-full mr-2">
    <div class="relative flex w-full">
      <TheSearchInput
        v-model:query="query"
        @change-state="toggleSearchResults"
        :has-results="results.length"
      />
      <TheSearchResults
        v-show="isSearchResultsShown"
        :results="results"
      />
    </div>

    <TheSearchButton />
  </div>
</template>
