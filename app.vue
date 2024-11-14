<script setup>
	import { ref, computed, onMounted } from 'vue';
	import ContactList from '@/components/ContactList.vue';
	import ContactForm from '@/components/ContactForm.vue';
	import SearchBar from '@/components/SearchBar.vue';

	const contacts = ref([]);
	const searchQuery = ref('');
	const currentContact = ref(null);
	const editingIndex = ref(null);

	onMounted(() => {
	const storedContacts = localStorage.getItem('contacts');
	if (storedContacts) {
		contacts.value = JSON.parse(storedContacts);
	}
	});

	const filteredContacts = computed(() => {
	return contacts.value.filter(contact => 
		contact.name.toLowerCase().includes(searchQuery.value.toLowerCase())
	);
	});

	const addContact = (contact) => {
	contacts.value.push(contact);
	saveContacts();
	};

	const updateContact = (contact) => {
	if (editingIndex.value !== null) {
		contacts.value[editingIndex.value] = contact;
		editingIndex.value = null; // Сбросить индекс после обновления
	} else {
		addContact(contact);
	}
	saveContacts();
	};

	const setCurrentContact = (index) => {
	currentContact.value = { ...contacts.value[index] }; // Копируем контакт для редактирования
	editingIndex.value = index; // Устанавливаем индекс редактируемого контакта
	};

	const deleteContact = (index) => {
	contacts.value.splice(index, 1);
	saveContacts();
	};

	const handleSearch = (query) => {
	searchQuery.value = query;
	};

	const saveContacts = () => {
	localStorage.setItem('contacts', JSON.stringify(contacts.value));
	};
</script>


<template>
	<div class="wrapper" id="app">

		<Header/>

		<main class="page">

			<section class="page__control control">
				<div class="control__container">

					<h1 class="control__title">Управление контактами</h1>

					<div class="control__form">

						<SearchBar @search="handleSearch" />

						<ContactForm 
							@addContact="addContact" 
							@editContact="updateContact" 
							:currentContact="currentContact" 
						/>

						<div class="control__result result-control">
							<div class="result-control__title">Добавленные контакты</div>

							<ContactList 
								:contacts="filteredContacts" 
								@editContact="setCurrentContact" 
								@deleteContact="deleteContact" 
							/>

						</div>

					</div>

				</div>
			</section>

		</main>

	  <!-- <h1>Управление контактами</h1>
	  <SearchBar @search="handleSearch" />
	  <ContactForm 
		 @addContact="addContact" 
		 @editContact="updateContact" 
		 :currentContact="currentContact" 
	  />
	  <ContactList 
		 :contacts="filteredContacts" 
		 @editContact="setCurrentContact" 
		 @deleteContact="deleteContact" 
	  /> -->

	</div>
	
 </template>
 
 <style lang="scss">

	.control {

			&__container {
			}

			&__title {
				font-size: 1.625rem;
				font-weight: 700;
				line-height: 2.1875rem;
				color: #000;
				text-align: center;
				&:not(:last-child){
					margin-bottom: 2.1875rem;
				}
			}
			&__form {
				display: flex;
				flex-direction: column;
				gap: 2.1875rem;
				max-width: 50rem;
				width: 100%;
				margin: 0 auto;
			}
			&__search {

			}
			&__add {
			}
			&__result {
			}
	}

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

	.result-control {
		&__title {
			font-size: 1.4375rem;
			font-weight: 500;
			&:not(:last-child){
				margin-bottom: 1.5625rem;
			}
		}
	}








 /* //======================================================================================================================================================== */
 
	.page {
		&__control {
			padding: 3.4375rem 0 5.3125rem 0;
		}
	}

 </style>