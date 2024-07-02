<script>
export default {
  data() {
    return {
      message: "Vue Jobs",
      status: "active",
      tasks: ["task one", "task two", "task three"],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <main>
    <h1>{{ message }}</h1>

    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>

    <!-- <a v-bind:href="link" target="_blank">Google</a> -->
    <a :href="link" target="_blank">Google</a>

    <br />

    <!-- <button v-on:click="toggleStatus">Change Status</button> -->
    <button @click="toggleStatus">Change Status</button>
  </main>
</template>
