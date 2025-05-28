<script setup>
import { computed, ref } from 'vue'
import Thing from './Thing.vue'

const leftThings = [
	{
		id: 1,
		name: 'Shoes 1',
	},
	{
		id: 2,
		name: 'Shoes 2',
	},
	{
		id: 3,
		name: 'Shoes 3',
	},
	{
		id: 4,
		name: 'Shoes 4',
	},
	{
		id: 5,
		name: 'T-shirt 1',
	},
	{
		id: 6,
		name: 'T-shirt 2',
	},
	{
		id: 7,
		name: 'T-shirt 3',
	},
	{
		id: 8,
		name: 'T-shirt 4',
	},
]
const rightThings = [
	{
		id: 11,
		name: 'Jacket 1',
	},
	{
		id: 12,
		name: 'Jacket 2',
	},
	{
		id: 13,
		name: 'Jacket 3',
	},
	{
		id: 14,
		name: 'Jacket 4',
	},
	{
		id: 15,
		name: 'Hoodie 1',
	},
	{
		id: 16,
		name: 'Hoodie 2',
	},
	{
		id: 17,
		name: 'Hoodie 3',
	},
	{
		id: 18,
		name: 'Hoodie 4',
	},
]

const selectedLeft = ref([])
const selectedRight = ref(null)

const selectedLeftThings = computed(() => {
	return leftThings.filter(t => selectedLeft.value.includes(t.id))
})
const selectedRightThings = computed(() => {
	return rightThings.filter(t => selectedRight.value === t.id)
})

const onSelectLeft = id => {
	if (!selectedLeft.value.includes(id) && selectedLeft.value.length < 6) {
		selectedLeft.value = [...selectedLeft.value, id]
	} else if (selectedLeft.value.includes(id)) {
		selectedLeft.value = selectedLeft.value.filter(s => s !== id)
	}
}
const onSelectRight = id => {
	if (selectedRight.value === id) {
		selectedRight.value = null
	} else {
		selectedRight.value = id
	}
}
</script>

<template>
	<div class="max-w-5xl p-6 m-auto flex flex-col gap-3">
		<div class="flex gap-3 p-3 justify-between border border-gray-500">
			<div class="w-36 min-h-36 border border-gray-500">
				<div
					v-for="th in selectedLeftThings"
					:key="th.id"
					class="p-3 border-2 border-gray-500"
				>
					{{ th.name }}
				</div>
			</div>
			<div class="w-36 min-h-36 border border-gray-500">
				<div
					v-for="th in selectedRightThings"
					:key="th.id"
					class="p-3 border-2 border-gray-500"
				>
					{{ th.name }}
				</div>
			</div>
		</div>
		<div class="flex gap-3 p-3 justify-between border border-gray-500">
			<div
				class="min-h-36 w-1/2 flex-1 flex flex-wrap gap-3 p-3 border border-gray-500"
			>
				<Thing
					v-for="th in leftThings"
					:="th"
					:key="th.id"
					:selected="selectedLeft.includes(th.id)"
					@select="onSelectLeft"
				/>
			</div>
			<div
				class="min-h-36 w-1/2 flex-1 flex flex-wrap gap-3 p-3 border border-gray-500"
			>
				<Thing
					v-for="th in rightThings"
					:="th"
					:key="th.id"
					:selected="selectedRight === th.id"
					@select="onSelectRight"
				/>
			</div>
		</div>
	</div>
</template>

<style scoped></style>
