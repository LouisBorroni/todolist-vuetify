<script lang="ts" setup>
import type { Task } from '@/types/Task';

defineProps<{
  tasks: Task[];
}>();

defineEmits<{
  (e: 'delete-task', id: number): void;
  (e: 'toggle-done', id: number): void;
  (e: 'edit-task', task: Task): void;
}>();
</script>

<template>
  <v-container>
    <v-row dense>
      <v-col
        v-for="task in tasks"
        :key="task.id"
        cols="12"
        md="6"
        lg="4"
      >
        <v-card
          :class="{ 'done-task': task.done }"
          class="pa-4 task-card"
          elevation="3"
          @click="$emit('toggle-done', task.id)"
        >
          <v-card-title class="d-flex justify-between align-center">
            <span class="font-weight-medium text-wrap" :class="{ 'text-decoration-line-through': task.done }">
              {{ task.title }}
            </span>
            <v-chip
              v-if="task.done"
              color="green"
              text-color="white"
              label
              small
              class="ml-2"
            >
              Fait
            </v-chip>
          </v-card-title>

          <v-card-text class="text--secondary">
            {{ task.description }}
          </v-card-text>

          <v-card-actions class="justify-end">
            <v-btn icon @click.stop="$emit('edit-task', task)">
              <v-icon color="blue">mdi-pencil</v-icon>
            </v-btn>
            <v-btn icon @click.stop="$emit('delete-task', task.id)">
              <v-icon color="red">mdi-delete</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>
.task-card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  cursor: pointer;
}
.task-card:hover {
  transform: scale(1.02);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}
.done-task {
  background-color: #f0fdf4;
  border-left: 6px solid #4caf50;
}
.text-decoration-line-through {
  text-decoration: line-through;
}
</style>
