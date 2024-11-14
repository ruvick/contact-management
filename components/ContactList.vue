<script setup>
	import { defineProps } from 'vue';

	const props = defineProps({
	contacts: {
		type: Array,
		required: true
	}
	});

	const emit = defineEmits(['editContact', 'deleteContact']);

	const editContact = (index) => {
	emit('editContact', index);
	};

	const deleteContact = (index) => {
	emit('deleteContact', index);
	};
</script>


<template>

<!-- <div class="add-control__inner"> -->

<!-- <button type="button" class="add-control__btn btn">Редактировать</button> -->
<!-- </div> -->

	<div class="result-control__list">
	  <div class="result-control__inner" v-for="(contact, index) in contacts" :key="contact.id">

			<div class="result-control__line">
				<div class="result-control__item">
					{{ contact.name }}
				</div>
				<div class="result-control__item">
					{{ contact.phone }}
				</div>
				<div class="result-control__item">
					{{ contact.email }}
				</div>
			</div>

			<div class="result-control__buttons">
				<button class="result-control__btn btn" @click="editContact(index)">Редактировать</button>
				<button class="result-control__btn btn" @click="deleteContact(index)">Удалить</button>
			</div>

		</div>
	</div>

 </template>
 
 <style scoped lang="scss">
 		.result-control {
			&__title {
				font-size: 1.4375rem;
				font-weight: 500;
				&:not(:last-child){
					margin-bottom: 0.9375rem;
				}
			}
			&__list {
			}

			&__inner {
				&:not(:last-child){
					margin-bottom: 2.1875rem;
				}
			}
			&__line {
				display: grid; 
				grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); 
				gap: 0.625rem;
				&:not(:last-child){
					margin-bottom: 1.25rem;
				}
			}
			&__item {
				font-size: 1rem;
				font-weight: 500;
				padding: 1.125rem 0.9375rem;
				background-color: rgba(2, 0, 32, 0.1490196078);
			}
			&__buttons {
				display: grid; 
				grid-template-columns: repeat(auto-fit, minmax(9.375rem, 1fr)); 
				gap: 0.625rem;
			}
			&__btn {

			}
	}
 </style>