<script setup>
import Button from './button.vue';
import Input from './input.vue';
import IconLocation from '../icons/location-icon.vue';
import { ref, inject } from 'vue';
import { cityProvide } from '../constants.js';

let isEdited = ref(false);
const city = inject(cityProvide);
const inputValue = ref(city.value);

function edit() {
	isEdited.value = true;
}

function select() {
	isEdited.value = false;
	city.value = inputValue.value;
}
</script>
<template>
	<div class="city-select">
		<div v-if="isEdited" class="city-input">
			<Input v-model="inputValue" v-focus placeholder="Enter city" @keyup.enter="select()" />
			<Button @click="select()">Save</Button>
		</div>
		<Button v-else @click="edit()">
			<IconLocation />
			Choose city
		</Button>
	</div>
</template>
<style scoped>
.city-input {
	display: flex;
	gap: 12px;

	width: 420px;
}
.city-select {
	width: 420px;
}
</style>
