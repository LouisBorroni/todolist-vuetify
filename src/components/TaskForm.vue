<script lang="ts" setup>
import { ref } from 'vue';

const title = ref('');
const description = ref('');

const emit = defineEmits<{
  (e: 'submit-task', task: { title: string; description: string }): void;
}>();

function submitForm() {
  emit('submit-task', {
    title: title.value,
    description: description.value
  });
  title.value = '';
  description.value = '';
}
</script>

<template>
  <v-form @submit.prevent="submitForm">
    <v-text-field v-model="title" label="Titre de la tâche" required />
    <v-textarea v-model="description" label="Description de la tâche" required />
    <v-btn type="submit" color="secondary">Ajouter la tâche</v-btn>
  </v-form>
</template>


