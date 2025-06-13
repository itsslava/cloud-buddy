<script setup></script>

<template>
	<button class="button"><slot></slot></button>
</template>

<style scoped>
.button {
	border: none;
	border-radius: 10px;
	text-align: center;
	padding: 14px;
	background: var(--gradient);
	color: var(--color-primary);
	font-weight: 600;
	font-size: 20px;
	font-family: var(--font);
	cursor: pointer;

	height: 53px;

	width: 100%;

	display: flex;
	gap: 9px;
	align-items: center;
	justify-content: center;
}

.button:hover {
	background: var(--gradient-inverted);
	transition: all 1s ease-out;
}
</style>
