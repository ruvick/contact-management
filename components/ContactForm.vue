<template>
	<form @submit.prevent="submitForm">
	  <input v-model="name" placeholder="Имя" required />
	  <input v-model="phone" placeholder="Телефон" required />
	  <input v-model="email" type="email" placeholder="Email" required />
	  <button type="submit">{{ isEditing ? 'Обновить' : 'Добавить' }}</button>
	</form>
 </template>
 
 <script setup>
 import { ref, watch, defineProps, defineEmits } from 'vue';
 
 const props = defineProps({
	currentContact: {
	  type: Object,
	  default: null
	}
 });
 
 const emit = defineEmits(['addContact', 'editContact']);
 
 const name = ref('');
 const phone = ref('');
 const email = ref(''); // Добавлено поле для email
 const isEditing = ref(false);
 
 watch(() => props.currentContact, (newValue) => {
	if (newValue) {
	  name.value = newValue.name;
	  phone.value = newValue.phone;
	  email.value = newValue.email; // Заполнение поля email при редактировании
	  isEditing.value = true;
	} else {
	  resetForm();
	}
 });
 
 const submitForm = () => {
	const contactData = { name: name.value, phone: phone.value, email: email.value }; // Добавлено поле email
	
	if (isEditing.value) {
	  emit('editContact', contactData);
	} else {
	  emit('addContact', contactData);
	}
	
	resetForm();
 };
 
 const resetForm = () => {
	name.value = '';
	phone.value = '';
	email.value = ''; // Сброс поля email
	isEditing.value = false;
 };
 </script>
 
 <style scoped>
 /* Стили для формы */
 </style>