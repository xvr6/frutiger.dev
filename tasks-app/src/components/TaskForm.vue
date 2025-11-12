<script lang="ts" setup>
import { ref } from "vue";

//this is effectively telling any component that imports it, that it emits an event.
//AKA, returns a value.
const emit = defineEmits<{
  addTask: [newTask: string];
}>();

const newTask = ref("");
const error = ref("");

function formSubmitted() {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
  } else {
    error.value = "Task can not be empty!";
  }
}
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <!-- on submit, run function. Prevent default action (in this case, reloading page) -->
    <label>
      New Task
      <input
        v-model="newTask"
        name="newTask"
        :aria-invalid="!!error || undefined"
        @input="error = ''"
      />
      <small v-if="error" id="invalid-helper">
        <!-- part of picocss. -->
        {{ error }}
      </small>
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>

<style scoped>
.button-container {
  display: flex;
  justify-content: end;
}
</style>
