<script setup>
import SunnyIcon from '../icons/weather/sunny-icon.vue';
import CloudyIcon from '../icons/weather/cloudy-icon.vue';
import RainyIcon from '../icons/weather/rainy-icon.vue';

import { computed } from 'vue';

const { weatherCode, temp, date, isActive } = defineProps({
	weatherCode: Number,
	temp: Number,
	date: Date,
	isActive: Boolean,
});

const iconColor = computed(() => {
	return isActive ? 'var(--color-primary-inverted)' : 'var(--color-primary)';
});
</script>
<template>
	<button class="weather-card" :class="{ active: isActive }">
		<SunnyIcon v-if="weatherCode <= 1003" :color="iconColor" />
		<CloudyIcon v-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor" />
		<RainyIcon v-if="weatherCode >= 1063" :color="iconColor" />

		<div class="weather-card__date">
			{{ date.toLocaleDateString('en-EN', { weekday: 'short' }) }}
		</div>
		<div class="weather-card__temp">{{ temp }} °C</div>
	</button>
</template>
<style scoped>
.weather-card {
	width: 100%;
	color: var(--color-primary);
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;

	border-radius: 10px;
	box-shadow: 1px 2px 4px 0 #222831;

	padding: 20px 24px;

	border: none;
	cursor: pointer;

	gap: 15px;
	background: var(--color-bg-card);
}
.active {
	background: var(--color-primary);
	color: var(--color-primary-inverted);
}
.weather-card:not(.active):hover {
	background: #3a434f;
}
.weather-card__date {
	font-size: 20px;
}
.weather-card__temp {
	font-weight: 700;
	font-size: 20px;
}
</style>
