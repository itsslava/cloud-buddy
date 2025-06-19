<script setup>
import { ref, computed } from 'vue';
import Stat from './components/stat.vue';

import CitySelect from './components/city-select.vue';

const data = ref({ humidity: 90, precipitation: 0, wind: 3 });

const dataModified = computed(() => {
	return [
		{ label: 'Humidity', stat: data.value.humidity + '%' },
		{ label: 'Precipitation', stat: data.value.precipitation + '%' },
		{ label: 'Wind', stat: data.value.wind + ' m/h' },
	];
});

let savedCity = ref('Техас');

function getCity(city) {
	savedCity.value = city;
}
</script>

<template>
	<main class="right-panel">
		<Stat v-for="item in dataModified" v-bind="item" :key="item.label" />
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
