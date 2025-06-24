<script setup>
import { computed, inject } from 'vue';

import { cityProvide } from '../constants.js';

import RainyIcon from '../icons/weather/rainy-icon.vue';
import CloudyIcon from '../icons/weather/cloudy-icon.vue';
import SunnyIcon from '../icons/weather/sunny-icon.vue';
import LocationIcon from '../icons/location-icon.vue';

const { dayData } = defineProps({
	dayData: Object,
});

const city = inject(cityProvide);

const weekday = computed(() => {
	return new Date(dayData.date).toLocaleDateString('en-EN', { weekday: 'long' });
});
const date = computed(() => {
	return new Date(dayData.date).toLocaleDateString('en-EN', {
		day: 'numeric',
		month: 'long',
		year: 'numeric',
	});
});

const weatherCode = computed(() => {
	return dayData.day.condition.code;
});
</script>
<template>
	<div class="panel-left">
		<div class="stat">
			<h1 class="day">
				{{ weekday }}
			</h1>
			<div class="date">
				{{ date }}
			</div>
			<div class="location">
				<LocationIcon size="27" />
				<span>{{ city }}</span>
			</div>
		</div>
		<div class="weather">
			<div>
				<SunnyIcon v-if="weatherCode <= 1003" :size="95" />
				<CloudyIcon v-if="weatherCode >= 1006 && weatherCode < 1063" :size="95" />
				<RainyIcon v-if="weatherCode >= 1063" :size="95" />
			</div>
			<div class="temp">{{ dayData.day.avgtemp_c }} °C</div>
			<div class="condition">{{ dayData.day.condition.text }}</div>
		</div>
	</div>
</template>
<style scoped>
.panel-left {
	display: flex;
	flex-direction: column;
	padding: 48px 32px;

	justify-content: space-between;
	height: 100%;
}

.stat {
	display: flex;
	flex-direction: column;
}
.day {
	font-weight: 700;
	font-size: 37px;
	margin-bottom: 16px;
}
.date {
	font-weight: 500;
	font-size: 22px;
	margin-bottom: 10px;
}
.location {
	display: flex;
	align-items: center;
	gap: 9px;

	text-transform: capitalize;
	font-weight: 600;
	font-size: 20px;
}

.weather {
	display: flex;
	flex-direction: column;
	align-items: flex-start;
	gap: 10px;
}

.temp {
	font-weight: 700;
	font-size: 50px;
}

.condition {
	font-weight: 700;
	font-size: 30px;
}
</style>
