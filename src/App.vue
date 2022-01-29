<template>
  <Timer />
  <!-- <Todo title="Todo App" /> -->
</template>

<script>
import Todo from "./components/Todo.vue";
import Timer from "./components/Timer.vue";

export default {
  name: "App",
  components: {
    Todo,
    Timer,
  },
};
</script>
