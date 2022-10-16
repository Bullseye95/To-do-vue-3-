<template>
  <task v-bind:tasks="tasks"></task>
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Workout",
          completed: true,
        },
        {
          id: 2,
          title: "Vue practice",
          completed: true,
        },
        {
          id: 3,
          title: "Eat food",
          completed: false,
        },
      ],
    };
  },
};
</script>
