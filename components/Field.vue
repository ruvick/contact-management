<script setup>
	import { defineProps, defineEmits } from 'vue';

	const props = defineProps({
	modelValue: String,
	label: String,
	name: String,
	placeholder: String,
	minlength: Number,
	type: String,
	});

	const emit = defineEmits(['update:modelValue']);

	const updateValue = (event) => {
	emit('update:modelValue', event.target.value);
	};
</script>

<template>
	<div class="field">
			<input
				:id="`input-${name}`"
				class="field__input"
				:name="name"
				:type="type"
				:placeholder="placeholder"
				:minlength="minlength"
				:value="modelValue"
				@input="updateValue"
				required
			/>
			<label :for="`input-${name}`" class="field__label">
				{{ label }} <span>*</span>
			</label>
	</div>
</template>

<style scoped lang="scss">
	.field {
		position: relative;
		overflow: hidden;
		width: 100%;
	}
	.field__input {
		display: block;
		margin: 0;
		padding: 0px 2.4375rem 0 0.9375rem;
		color: inherit;
		width: 100%;
		font-family: inherit;
		font-size: 1rem;
		font-weight: inherit;
		border: none;
		color: #000;
		transition: all 0.3s ease 0s;
		height: 3.125rem;
		border-radius: 0.1875rem;
		background-color: rgba(2, 0, 32, 0.03);
		transition: all 0.3s ease 0s;
	}
	@media (any-hover: hover) {
		.field__input:hover { 
			background-color: #02002026;
		} 
	}
	.field__label {
		font-size: 0.75rem;
		text-transform: uppercase;
		color: #65657b;
		left: 1.25rem;
		line-height: 0.875rem;
		pointer-events: none;
		position: absolute;
		transform-origin: 0 50%;
		transition: transform 200ms, color 200ms;
		top: 1.25rem;
		span {
			display: inline-block;
			color: red;
			transform: translateY(-0.125rem);
		}
	}
	.field__input:focus ~ .field__label,
	.field__input:not(:placeholder-shown) ~ .field__label {
		transform: translateY(-0.9375rem) translateX(-0.3125rem) scale(0.65);
	}
</style>
