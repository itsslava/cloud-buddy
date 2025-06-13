<script setup>
import { ref } from 'vue';
import Stat from './components/stat.vue';

import CitySelect from './components/city-select.vue';

const label = 'Влажность';
const stat = '90%	';

const data = {
	label: 'Осадки',
	stat: '0%',
};

let savedCity = ref('Техас');

function getCity(city) {
	savedCity.value = city;
}
</script>

<template>
	<main class="right-panel">
		{{ savedCity }}
		<Stat :label="label" :stat="stat" />
		<Stat v-bind="data" />
		<Stat label="Ветер" stat="3 м/ч" />
		<CitySelect @select-city="getCity" />
	</main>
</template>

<style scoped>
.right-panel {
	background: var(--color-bg-main);

	padding: 60px 50px;

	border-radius: 25px;
}
</style>
