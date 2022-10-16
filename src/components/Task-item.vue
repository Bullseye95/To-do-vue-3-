<template>
  <li>
    <button @click.self="$emit('complete')" :class="className">
      <font-awesome-icon @click.self="$emit('complete')" :icon="iconName" />
      {{ task.title }}
    </button>
    <button @click="$emit('remove')">
      <i class="far fa-trash-alt"></i>
    </button>
  </li>
</template>

<script>
export default {
  name: "TaskItem",
  props: ["task"],
  computed: {
    iconName() {
      return this.task.completed ? "fa-regular fa-circle-check" : "fa-regular fa-circle";
    },
    className() {
      let classes = ["toggle"];
      if (this.task.completed) {
        classes.push("toggle-completed");
      }
      return classes.join(" ");
    },
  },
};
</script>
