<!-- eslint-disable no-undef -->
<script setup>
import { ref, computed } from 'vue';

import Stat from './components/stat.vue';
import Error from './components/error.vue';
import CitySelect from './components/city-select.vue';
import WeatherCard from './components/weather-card.vue';

const API_ENDPOINT = 'https://api.weatherapi.com/v1';

let data = ref();
let error = ref();
let activeIndex = ref(0);

const dataModified = computed(() => {
	return [
		{ label: 'Humidity', stat: data.value.current.humidity + ' %' },
		{ label: 'Cloud', stat: data.value.current.cloud + ' %' },
		{ label: 'Wind', stat: data.value.current.wind_mph + ' m/h' },
	];
});

async function getCity(city) {
	const params = new URLSearchParams({
		q: city,
		lang: 'en',
		key: '834aa3a2cc8a4c53a94103958230906',
		days: 3,
	});
	const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);
	if (res.status != 200) {
		error.value = await res.json();
		data.value = null;
		return;
	}
	error.value = null;
	data.value = await res.json();
	console.log(data.value);
}
</script>

<template>
	<main class="right-panel">
		<Error :error="error?.error?.message" />
		<div v-if="data" class="weather-info">
			<div class="weather-stat">
				<Stat v-for="item in dataModified" v-bind="item" :key="item.label" />
			</div>
			<div class="weather-card-list">
				<WeatherCard
					v-for="(item, i) in data.forecast.forecastday"
					:key="item.date"
					:weather-code="item.day.condition.code"
					:temp="item.day.avgtemp_c"
					:date="new Date(item.date)"
					:is-active="activeIndex == i"
					@click="() => (activeIndex = i)"
				/>
			</div>
		</div>
		<CitySelect @select-city="getCity" />
	</main>
</template>

<style scoped>
.right-panel {
	background: var(--color-bg-main);
	padding: 60px 50px;
	border-radius: 25px;
}
.weather-card-list {
	display: flex;
	gap: 1px;
}
.weather-info {
	display: flex;
	flex-direction: column;
	gap: 80px;
	margin-bottom: 70px;
}
.weather-stat {
	display: flex;
	flex-direction: column;
	gap: 16px;
}
</style>
