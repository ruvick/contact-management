<script setup>
	import { ref } from 'vue';

	const emit = defineEmits(['search']);
	const query = ref('');

	const search = () => {
		emit('search', query.value);
	};
</script>

<template>

	<div class="search-control">
		<div class="search-control__title">Найти контакт</div>
		<div class="search-control__form form-search">
			<input class="form-search__input" v-model="query" placeholder="Поиск контактов..." />
			<button type="button" class="form-search__btn btn" @click="search">Найти</button>
		</div>
	</div>

 </template>
 
 <style scoped lang="scss">
	.search-control {
		&__title {
			font-size: 1.4375rem;
			font-weight: 500;
			&:not(:last-child){
				margin-bottom: 0.9375rem;
			}
		}
		&__form {
		}
		&__btn {
		}
	}

	.form-search {
		position: relative;
		background: rgba(2, 0, 32, .03);
		overflow: hidden;
		&__input {
			width: 100%;
			font-size: 1rem;
			height: 2.5rem;
			color: grey;
			background-color: inherit;
			padding: 0.3125rem 0.9375rem;
		}
		&__btn {
			position: absolute;
			top: 50%;
			right: 0;
			transform: translateY(-50%);
		}
	}
</style>