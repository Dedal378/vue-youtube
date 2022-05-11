<script setup>
import { onMounted, ref } from 'vue'
import BaseIcon from './BaseIcon.vue'

const searchInput = ref(null)
const classes = [
  'px-3',
  'w-full',
  'h-full',
  'border',
  'border-gray-300',
  'shadow-inner',
  'rounded-bl-sm',
  'rounded-tl-sm',
  'focus:border-blue-700',
  'focus:outline-none',
]

const props = defineProps(['query', 'queryModifiers'])
const emits = defineEmits(['update:query'])

const updateQuery = (query) => {
  if (props.queryModifiers['no-spaces']) {
    query = query.replace(/\s+/g, ' ').trim()
  }

  emits('update:query', query)
}

onMounted(() => {
  if (window.innerWidth < 640) {
    searchInput.value.focus()
  }
})
</script>

<template>
  <div class="relative w-full">
    <input
      @input="updateQuery($event.target.value)"
      :class="classes"
      :value="query"
      ref="searchInput"
      placeholder="Search"
      type="text"
    />

    <button
      v-show="query"
      @click="updateQuery('')"
      class="absolute top-0 right-0 h-full px-3 focus:outline-none"
    >
      <BaseIcon
        name="x"
        class="w-5 h-5"
      />
    </button>
  </div>
</template>
