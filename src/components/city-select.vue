<script setup>
import Button from './button.vue';
import InputView from './input-view.vue';
import IconLocation from '../icons/location-icon.vue';
import { ref } from 'vue';
import { defineEmits } from 'vue';

const emit = defineEmits({
	selectCity(payload) {
		return payload;
	},
});

let isEdited = ref(false);

let city = ref('Texas');

function edit() {
	isEdited.value = true;
}

function select() {
	isEdited.value = false;
	emit('selectCity', 'Paris');
}
</script>
<template>
	<div class="city-select">
		{{ city }}
		<div v-if="isEdited" class="city-input">
			<!-- <InputView v-model="city" v-model:additional="city" placeholder="Enter city" /> -->
			<InputView v-model="city" v-model:additional="city" placeholder="Enter city" />
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
