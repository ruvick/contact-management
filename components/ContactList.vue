<template>
	<ul>
	  <li v-for="(contact, index) in contacts" :key="contact.id">
		 {{ contact.name }} - {{ contact.phone }} - {{ contact.email }}
		 <button @click="editContact(index)">Редактировать</button>
		 <button @click="deleteContact(index)">Удалить</button>
	  </li>
	</ul>
 </template>
 
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
 
 <style scoped>
 /* Стили для списка контактов */
 </style>