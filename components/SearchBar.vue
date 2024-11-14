<template>
	<div>
	  <input v-model="query" placeholder="Поиск контактов..." />
	  <button @click="search">Поиск</button>
	</div>
 </template>
 
 <script setup>
 import { ref } from 'vue';
 
 const emit = defineEmits(['search']);
 const query = ref('');
 
 const search = () => {
	emit('search', query.value);
 };
 </script>
 
 <style scoped>
 /* Стили для поля поиска */
 </style>