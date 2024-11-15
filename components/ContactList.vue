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
  <div class="result-control__list">
    <transition-group name="fade" tag="div">
      <div 
        class="result-control__inner" 
        v-for="(contact, index) in contacts" 
        :key="contact.id"
      >
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
					<Button class="result-control__btn btn" @click="editContact(index)">Редактировать</Button>
          <Button class="result-control__btn btn--delete" @click="deleteContact(index)">Удалить</Button>
        </div>
      </div>
      <div v-if="contacts.length === 0" class="no-results-message">Контакты не найдены</div> 
    </transition-group>
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
				@media (max-width: 48em){
					  font-size: 1.125rem;
				}
			}
			&__inner {
				&:not(:last-child){
					margin-bottom: 2.1875rem;
				}
			}
			&__line {
				display: grid; 
				grid-template-columns: repeat(auto-fit, minmax(12.5rem, 1fr)); 
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
				@media (max-width: 48em){
					font-size: 0.875rem;
					padding: 0.875rem 0.9375rem;
				}
			}
			&__buttons {
				display: grid; 
				grid-template-columns: repeat(auto-fit, minmax(12.5rem, 1fr)); 
				gap: 0.625rem;
			}
	}
	.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
	}
	.fade-enter, .fade-leave-to {
		opacity: 0;
	}
	.fade-enter-from {
		opacity: 0;
	}
	.fade-enter-to {
		opacity: 1;
	}
 </style>