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
	const email = ref(''); 
	const isEditing = ref(false);

	watch(() => props.currentContact, (newValue) => {
		if (newValue) {
			name.value = newValue.name;
			phone.value = newValue.phone;
			email.value = newValue.email; 
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
		email.value = ''; 
		isEditing.value = false;
	};
</script>

<template>
	<div class="control__add add-control">
		<div class="add-control__title">Добавить контакт</div>
		<form @submit.prevent="submitForm" class="add-control__inner">

			<div class="add-control__field field">
				<input id="input" class="field__input" name="form[]" autocomplete="off" type="name" placeholder=" " 
					data-error="Заполните поле" data-required="name" data-validate v-model="name" minlength="3" required>
				<label for="input" class="field__label">Имя <span>*</span></label>
			</div>

			<div class="add-control__field field">
				<input id="input" class="field__input" name="tel" autocomplete="off" type="number" placeholder=" " 
				data-error="Заполните поле" data-required="tel" data-validate v-model="phone" minlength="10" required>
				<label for="input" class="field__label">Телефон <span>*</span></label>
			</div>

			<div class="add-control__field field">
				<input id="input" class="field__input" name="email" autocomplete="off" placeholder=" " 
				data-error="Неверный Email" data-required="email" data-validate v-model="email" type="email" required>
				<label for="input" class="field__label">Email <span>*</span></label>
			</div>

			<Button type="submit" class="add-control__btn btn">
      	{{ isEditing ? 'Обновить' : 'Добавить' }}
    	</Button>

		</form>
	</div>
 </template>
 
 <style scoped lang="scss">
	.add-control {
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
		&__field {
			&:not(:last-child){
				margin-bottom: 0.625rem;
			}
		}
		&__btn {
			display: flex;
			margin-left: auto;
			@media (max-width: 25.875em){
				  margin: 0;
					width: 100%;
			}
		}
	}
 </style>