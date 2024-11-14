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

	<ul>
	  <li v-for="(contact, index) in contacts" :key="contact.id">
		 {{ contact.name }} - {{ contact.phone }} - {{ contact.email }}
		 <button @click="editContact(index)">Редактировать</button>
		 <button @click="deleteContact(index)">Удалить</button>
	  </li>
	</ul>

 </template>
 
 <style scoped lang="scss">
 		.add-control {
			&__title {
				font-size: 1.4375rem;
				font-weight: 500;
				&:not(:last-child){
					margin-bottom: 0.9375rem;
				}
			}
			&__inner {
			}
			&__field {
				&:not(:last-child){
					margin-bottom: 0.625rem;
				}
			}
			&__btn {
				display: flex;
				margin-left: auto;
			}
	}
 </style>