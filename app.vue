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

					<form class="control__form">

						<SearchBar @search="handleSearch" />

						<div class="control__add add-control">
							<div class="add-control__title">Добавить контакт</div>
							<div class="add-control__inner">

								<div class="add-control__field field">
									<input id="input" class="field__input" name="form[]" autocomplete="off" type="name" placeholder=" " 
										data-error="Заполните поле" data-required="name" data-validate>
									<label for="input" class="field__label">Имя <span>*</span></label>
								</div>

								<div class="add-control__field field">
									<input id="input" class="field__input" name="tel" autocomplete="off" type="number" placeholder=" " 
									data-error="Заполните поле" data-required="tel" data-validate>
									<label for="input" class="field__label">Телефон <span>*</span></label>
								</div>

								<div class="add-control__field field">
									<input id="input" class="field__input" name="email" autocomplete="off" type="text" placeholder=" " 
									data-error="Неверный Email" data-required="email" data-validate>
									<label for="input" class="field__label">Email <span>*</span></label>
								</div>

								<button type="button" class="add-control__btn btn">Добавить</button>

							</div>
						</div>

						<div class="control__add add-control">
							<div class="add-control__title">Добавленные контакты</div>

							<div class="add-control__inner">
								<button type="button" class="add-control__btn btn">Редактировать</button>
							</div>

						</div>

				</form>

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
 
 <style scoped lang="scss">

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








input[type="text"],
input[type="email"],
input[type="tel"],
textarea {
	width: 100%;
	outline: none;
	-webkit-appearance: none;
	-moz-appearance: none;
	appearance: none;
}

input[type=radio] {
	position: absolute;
	width: 0;
	height: 0;
	opacity: 0;
	left: 0;
	top: 0;
	visibility: hidden;
}

/* Убираем стрелки у цифрового инпута */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
	/* display: none; <- Crashes Chrome on hover */
	-webkit-appearance: none;
	margin: 0;
}

textarea.input {
	resize: none;
	padding: 0.3125rem 0.625rem;
	width: 100%;
}

/* Стилизация placeholder  */
::-webkit-input-placeholder {
	transition: all 0.3s ease 0s;
	color: rgba(2, 0, 32, 0.3);
}

::-moz-placeholder {
	transition: all 0.3s ease 0s;
	color: rgba(2, 0, 32, 0.3);
}

/* Firefox 19+ */
:-moz-placeholder {
	transition: all 0.3s ease 0s;
	color: rgba(2, 0, 32, 0.3);
}

/* Firefox 18- */
:-ms-input-placeholder {
	transition: all 0.3s ease 0s;
	color: rgba(2, 0, 32, 0.3);
}
/* //======================================================================================================================================================== */

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
 /* =================================================================================================================================== * */

 .checkbox {
	position: relative;
	display: block;
 }
 .checkbox__input {
	position: absolute;
	width: 0;
	height: 0;
	opacity: 0;
	visibility: hidden;
}
.checkbox__text {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	position: relative;
	font-size: 0.6875rem;
	font-weight: 400;
	line-height: 1.2857142857;
	letter-spacing: 0;
	text-transform: uppercase;
	color: #020020;
	cursor: pointer;
}
.checkbox__text:before {
	content: "";
	-ms-flex-item-align: start;
	align-self: flex-start;
	margin: 0;
	-webkit-box-flex: 0;
	-ms-flex: 0 0 1.25rem;
	flex: 0 0 1.25rem;
	left: 0;
	top: 0;
	width: 1.25rem;
	height: 1.25rem;
	background: 0 0;
	border: .0625rem solid rgba(2, 0, 32, .3);
	border-radius: .1875rem;
}
.checkbox__input:checked+.checkbox__text:before {
	content: "\e90c";
	font-size: .5rem;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	background: #120b8d;
	color: #fff;
	font-family: icons;
	font-style: normal;
	font-weight: 400;
	font-variant: normal;
	text-transform: none;
	line-height: 1;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
.checkbox__text span {
	margin-left: .625rem;
}
.checkbox__text a {
	font-size: 0.6875rem;
	font-weight: 400;
	line-height: 1.2857142857;
	letter-spacing: 0;
	color: #120b8d;
	text-decoration: none;
	-webkit-transition: all .4s ease 0s;
	transition: all .4s ease 0s;
}
.checkbox._form-error .checkbox__text:before {
	border: 0.0625rem solid red;
}
/* .checkbox._form-error .checkbox__text,
.checkbox._form-error .checkbox__text a {
	color: red;
} */
.checkbox .form__error {
	display: none;
}
 /* //======================================================================================================================================================== */
 
	.page {
		&__control {
			padding: 3.4375rem 0;
		}
	}

 </style>