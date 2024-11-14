<script setup>
	import { ref } from 'vue';

	const emit = defineEmits(['search']);
	const query = ref('');
	const errorMessage = ref(''); 

	const search = () => {
		emit('search', query.value);
	};
</script>

<template>
  <form class="search-control" @submit.prevent="search"> 
    <div class="search-control__title">Найти контакт</div>
    <div class="search-control__form form-search">
      <input 
        class="form-search__input" 
        v-model="query" 
        type="text" 
        placeholder="Поиск контактов..." 
        minlength="3" 
        required 
      > 
      <button type="submit" class="form-search__btn btn">Найти</button>
    </div>
    <div v-if="errorMessage" class="form-search__error-message">{{ errorMessage }}</div> 
  </form>
</template>
 
 <style scoped lang="scss">
	.search-control {
		&__title {
			font-size: 1.4375rem;
			font-weight: 500;
			&:not(:last-child){
				margin-bottom: 0.9375rem;
			}
			@media (max-width: 48em){
				  font-size: 1.125rem;
			}
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
			@media (max-width: 48em){
				font-size: 0.875rem;
			}
		}
		&__btn {
			position: absolute;
			top: 50%;
			right: 0;
			transform: translateY(-50%);
		}
		&__error-message {
			position: absolute;
			font-size: 0.75rem;
			color: red;
			margin-top: 0.5rem;
			margin-left: 0.9375rem;
		}
	}
</style>