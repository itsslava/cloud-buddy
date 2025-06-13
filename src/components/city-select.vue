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

function edit() {
	isEdited.value = true;
}

function select() {
	isEdited.value = false;
	emit('selectCity', 'Париж');
}
</script>
<template>
	<div class="city-select">
		<div v-if="isEdited" class="city-input">
			<InputView placeholder="Введите город" />
			<Button @click="select()">Сохранить</Button>
		</div>
		<Button v-else @click="edit()">
			<IconLocation />
			Изменить город
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
