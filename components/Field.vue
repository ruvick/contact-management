<script setup lang="ts">
	import { defineProps, computed } from 'vue';

	const props = defineProps({
		modelValue: {
			type: String,
			required: true,
		},
		label: {
			type: String,
			required: true,
		},
		name: {
			type: String,
			required: true,
		},
		placeholder: {
			type: String,
			default: '',
		},
		minlength: {
			type: Number,
			default: 3,
		},
		type: {
			type: String,
			default: 'text', 
		},
	});

	const inputId = computed(() => `input-${props.name}`); 
</script>

<template>
  <div class="add-control__field field">
    <input
      :id="inputId"
      class="field__input"
      :name="props.name"
      :type="props.type" 
      autocomplete="off"
      :placeholder="props.placeholder"
      v-model="props.modelValue"
      :minlength="props.minlength"
      required
    />
    <label :for="inputId" class="field__label">
      {{ props.label }} <span>*</span>
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
	
	.field__input:not(:placeholder-shown) ~ .field__label {
		/* color: #808097; */
	}
	
	.field__input:focus ~ .field__label {
		/* color: #dc2f55; */
	}

	/* Validation ======================================================================================================================== */

	.field._form-error .field__input {
		border: 0.0625rem solid red;
	}
	.field .form__error {
		display: block;
		font-size: 0.625rem;
		font-weight: 400;
		letter-spacing: 0em;
		color: red;
		margin-top: 0.3125rem;
	}
	.field:before {
		content: '';
		position: absolute;
		top: 50%;
		right: 0.8125rem;
		transform: translateY(-50%);
		width: 1.25rem;
		height: 1.25rem;
		background-repeat: no-repeat;
		background-position: center;
		background-size: 100%;
	}
	.field._check-focus:before {
		background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjUiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNSAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik0yMS4zMzQgNi40NzAxNkwxMC4yMDY4IDE4TDMuMzMzOTggMTAuODc4NEw0LjkyNDYzIDkuNDA4MjRMMTAuMjA2OCAxNC44ODE2TDE5Ljc0MzMgNUwyMS4zMzQgNi40NzAxNloiIGZpbGw9IiMwMEJGMzYiLz4KPC9zdmc+Cg==');
	}

	.field._form-error:before {
		top: 40%;
		width: 1.125rem;
		height: 1.125rem;
		background-image: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjUiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNSAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTIwLjMzMDUgMi41ODU5NEwxMi4zMzA1IDEwLjU4NTlMNC4zMzA1MiAyLjU4NTk0TDIuOTE2MDIgMy45OTk5NEwxMC45MTY1IDExLjk5OTlMMi45MTYwMiAxOS45OTk5TDQuMzMwNTIgMjEuNDEzOUwxMi4zMzA1IDEzLjQxMzlMMjAuMzMwNSAyMS40MTM5TDIxLjc0NDUgMTkuOTk5OUwxMy43NDQ1IDExLjk5OTlMMjEuNzQ0NSAzLjk5OTk0TDIwLjMzMDUgMi41ODU5NFoiIGZpbGw9InJlZCIvPgo8L3N2Zz4K');
	}
</style>
