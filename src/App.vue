<!-- eslint-disable no-undef -->
<script setup>
import { ref, provide, watch, onMounted } from 'vue';
import PanelRight from './components/panel-right.vue';
import { cityProvide, API_ENDPOINT } from './constants.js';

const data = ref([]);
const error = ref();
const activeIndex = ref(0);
const city = ref('Paris');

provide(cityProvide, city);

watch(city, () => {
	getCity(city.value);
});

onMounted(() => {
	getCity(city.value);
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
}
</script>

<template>
	<main class="main">
		<div class="left-panel"></div>
		<div class="right-panel">
			<PanelRight
				:data="data"
				:error="error"
				:active-index="activeIndex"
				@select-index="(i) => (activeIndex = i)"
			/>
		</div>
	</main>
</template>

<style scoped>
.main {
	display: flex;
	align-items: center;
	justify-content: center;
}
.right-panel {
	background: var(--color-bg-main);
	padding: 60px 50px;
	border-radius: 0 25px 25px 0;
}
.left-panel {
	width: 500px;
	height: 680px;
	border-radius: 30px;
	background-image: url('/public/right-panel.png');
	background-repeat: no-repeat;
	background-size: cover;
}
</style>
