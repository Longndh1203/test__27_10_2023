<template>
  <div id="app">
    <task-manager></task-manager>
  </div>
</template>

<script>
import TasksManage from "./components/TasksManage.vue";

export default {
  name: "App",
  components: {
    "task-manager": TasksManage,
  },
};
</script>

<style></style>
