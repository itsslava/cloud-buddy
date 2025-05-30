<script setup>
import Button from './components/button.vue';
import Stat from './components/stat.vue';

const label = 'Влажность';
const stat = '90%	';

const data = {
	label: 'Осадки',
	stat: '0%',
};
</script>

<template>
	<main class="right-panel">
		<Stat :label="label" :stat="stat" />
		<Stat v-bind="data" />
		<Stat label="Ветер" stat="3 м/ч" />
		<Button>Сохранить</Button>
	</main>
</template>

<style scoped>
.right-panel {
	background: var(--color-bg-main);

	padding: 60px 50px;

	border-radius: 25px;
}
</style>
