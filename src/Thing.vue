<script setup>
import { defineProps, defineEmits } from 'vue'
const props = defineProps({
	id: Number,
	name: String,
	selected: {
		type: Boolean,
		default: false,
	},
})
const emit = defineEmits(['select'])
</script>

<template>
	<div
		class="p-3 border-2 border-gray-500 hover:cursor-pointer"
		:class="{ 'bg-blue-300': selected }"
		@click="emit('select', id)"
	>
		{{ name }}
	</div>
</template>
