<script setup>
import { ref } from 'vue'

defineProps({
  results: {
    type: Array,
    required: false,
    default: null,
  },
})

const classes = ref([
  'absolute',
  'top-full',
  'w-full',
  'bg-white',
  'border',
  'border-t-0',
  'border-gray-300',
  'shadow-md',
  'pt-4',
  'select-none',
  'truncate',
])
const itemClasses = ref(['hover:bg-gray-100', 'text-black', 'px-3', 'py-1'])
const reportLinkClasses = ref([
  'w-full',
  'inline-block',
  'text-right',
  'text-xs',
  'italic',
  'text-gray-500',
  'hover:text-black pr-2',
])
</script>

<template>
  <div :class="classes">
    <ul>
      <li
        v-for="result in results"
        :key="result"
        :class="itemClasses"
      >
        {{ result }}
      </li>
    </ul>

    <a
      :class="reportLinkClasses"
      href="#"
    >
      Report search predictions
    </a>
  </div>
</template>
