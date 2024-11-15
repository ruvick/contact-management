<script setup lang="ts">
	import { defineProps } from 'vue';

	const props = defineProps({
		buttonClass: {
			type: String,
			default: 'btn', 
		},
		onClick: {
			type: Function,
			required: true,
		},
	});

	// Обработчик клика
	const handleClick = (event: MouseEvent) => {
		props.onClick(event);
	};
</script>

<template>
  <button :class="buttonClass" @click="handleClick">
    <slot></slot>
  </button>
</template>

<style scoped lang="scss">
	.btn {
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		padding: .90625rem 1.48125rem;
		font-size: 1rem;
		font-weight: 600;
		color: #fff;
		background-color: #120b8d;
		border-radius: .1875rem;
		transition: all .4s ease 0s;
		@media (max-width: 48em){
			font-size: 0.875rem;
			padding: 0.625rem 1.25rem;
		}
	}
	.btn--delete {
		opacity: 0.7;
	}
	@media (any-hover: hover){
		.btn:hover { 
			opacity: 0.7;
		} 
	}
</style>

