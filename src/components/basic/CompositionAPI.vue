<!-- <script>
import { ref } from "vue";

export default {
  setup() {
    const message = ref("Vue Jobs");
    const status = ref("active");
    const tasks = ref(["task one", "task two", "task three"]);
    const link = ref("https://google.com");

    const toggleStatus = () => {
      if (status.value === "active") {
        status.value = "pending";
      } else if (status.value === "pending") {
        status.value = "inactive";
      } else {
        status.value = "active";
      }
    };

    return {
      message,
      status,
      tasks,
      link,
      toggleStatus,
    };
  },
};
</script> -->

<script setup>
import { ref, onMounted } from "vue";

const message = ref("Vue Jobs");
const status = ref("active");
const tasks = ref(["task one", "task two", "task three"]);
const link = ref("https://google.com");

const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    throw error;
  }
});
</script>

<template>
  <main>
    <h1>{{ message }}</h1>

    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <form @submit.prevent="addTask">
      <label for="newTask">Add Task:</label>
      <input type="text" id="newTask" name="newTask" v-model="newTask" />
      <button type="submit">Submit</button>
    </form>

    <h3>Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>{{ task }}</span>
        <button @click="deleteTask(index)">X</button>
      </li>
    </ul>

    <!-- <a v-bind:href="link" target="_blank">Google</a> -->
    <a :href="link" target="_blank">Google</a>

    <br />

    <!-- <button v-on:click="toggleStatus">Change Status</button> -->
    <button @click="toggleStatus">Change Status</button>
  </main>
</template>
