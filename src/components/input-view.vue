<script setup></script>
<template><input class="input" /></template>
<style scoped>
.input {
	color: var(--color-white);
	border-radius: 10px;
	border: none;
	box-shadow: 1px 2px 4px 0px var(--color-bg-main);
	background: var(--color-bg-card);
	width: 260px;
	height: 53px;
	padding: 15px 20px;
	font-size: 18px;
}

.input::placeholder {
	color: var(--color-text-placeholder);
}
</style>
