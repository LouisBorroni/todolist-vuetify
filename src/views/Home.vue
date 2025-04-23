<template>
  <v-container>
    <h1 class="text-h4 mb-4">Accueil - Ajout</h1>
    <TaskForm @submit-task="addTask" />
  </v-container>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted, watch } from 'vue';
import type { Task } from '@/types/Task';
import TaskForm from '@/components/TaskForm.vue';

const tasks = ref<Task[]>([]);

const search = ref('');
const sortMode = ref<'Date' | 'État'>('Date');

const STORAGE_KEY = 'my-vue-tasks';

onMounted(() => {
  const saved = localStorage.getItem(STORAGE_KEY);
  if (saved) {
    tasks.value = JSON.parse(saved);
  }
});

watch(tasks, (newTasks) => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(newTasks));
}, { deep: true });

function addTask(task: { title: string; description: string }) {
  tasks.value.push({
    id: Date.now(),
    title: task.title,
    description: task.description,
    done: false
  });
}
</script>
