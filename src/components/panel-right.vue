<script setup>
import Stat from './stat.vue';
import Error from './error.vue';
import CitySelect from './city-select.vue';
import WeatherCard from './weather-card.vue';

import { computed } from 'vue';

const { error, data, activeIndex } = defineProps({
	error: Object,
	data: Object,
	activeIndex: Number,
});

const emit = defineEmits(['select-index', 'select-city']);

const statData = computed(() => {
	if (!data) {
		return [];
	}
	return [
		{ label: 'Humidity', stat: data.current.humidity + ' %' },
		{ label: 'Cloud', stat: data.current.cloud + ' %' },
		{ label: 'Wind', stat: data.current.wind_mph + ' m/h' },
	];
});
</script>
<template>
	<Error :error="error?.error?.message" />
	<div v-if="data.current" class="weather-info">
		<div class="weather-stat">
			<Stat v-for="item in statData" v-bind="item" :key="item.label" />
		</div>
		<div class="weather-card-list">
			<WeatherCard
				v-for="(item, i) in data.forecast.forecastday"
				:key="item.date"
				:weather-code="item.day.condition.code"
				:temp="item.day.avgtemp_c"
				:date="new Date(item.date)"
				:is-active="activeIndex == i"
				@click="() => emit('select-index', i)"
			/>
		</div>
	</div>
	<CitySelect />
</template>
<style scoped>
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
