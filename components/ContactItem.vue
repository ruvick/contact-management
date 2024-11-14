<template>
	<li>
	  <span>{{ contact.name }}</span> - 
	  <span>{{ contact.phone }}</span> - 
	  <span>{{ contact.email }}</span>
	  <button @click="$emit('edit')">Редактировать</button>
	  <button @click="$emit('delete')">Удалить</button>
	</li>
 </template>
 
 <script setup>
 import { defineProps } from 'vue';
 
 const props = defineProps({
	contact: Object
 });
 </script>
 
 <style scoped>
 /* Стили для элемента контакта */
 </style>