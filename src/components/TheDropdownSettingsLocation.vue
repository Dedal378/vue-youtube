<script setup>
import { ref } from 'vue'
import DropdownSettingsListItem from './DropdownSettingsListItem.vue'
import DropdownSettingsHeader from './DropdownSettingsHeader.vue'

defineProps({
  selectedOptions: {
    type: [Object, Number, String],
    required: false,
    default: 0,
  },
})
const emits = defineEmits(['select-menu', 'select-option'])
const locations = ref(['United States', 'Belarus', 'Ukraine', 'Russia'])
const selectOption = (location) => {
  emits('select-option', { name: 'location', value: location })
}
</script>

<template>
  <DropdownSettingsHeader
    title="Choose your location"
    @back="$emit('select-menu', 'main')"
  />

  <section class="py-2">
    <ul class="max-h-96 overflow-auto">
      <DropdownSettingsListItem
        @click.stop="selectOption({ id: locationIdx, text: location})"
        v-for="(location, locationIdx) in locations"
        :key="locationIdx"
        :active="locationIdx === selectedOptions.location.id"
        :label="location"
      />
    </ul>
  </section>
</template>
