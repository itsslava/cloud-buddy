<script setup>
import Button from './button.vue';
import Input from './input.vue';
import IconLocation from '../icons/location-icon.vue';
import { ref, onMounted } from 'vue';
import { defineEmits } from 'vue';

let isEdited = ref(false);

let city = ref('Paris');

const emit = defineEmits({
	selectCity(payload) {
		return payload;
	},
});

function edit() {
	isEdited.value = true;
}

onMounted(() => {
	emit('selectCity', city.value);
});

function select() {
	isEdited.value = false;
	emit('selectCity', city.value);
}
</script>
<template>
	<div class="city-select">
		<div v-if="isEdited" class="city-input">
			<Input v-model="city" v-focus placeholder="Enter city" @keyup.enter="select()" />
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
