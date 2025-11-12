<script lang="ts" setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types";

const message = ref("Tasks App");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
  //pushing to state variable is all vue needs to send updates to dom.
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @add-task="addTask" />
    <!-- on add-task being passed from taskform, execute function -->
    <h3 v-if="tasks.length > 0">There are {{ tasks.length }} task(s)</h3>
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
}
</style>
