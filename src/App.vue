<template>
  <Navbar v-on:toggleTodoApp="toggleApp($event)" :sTodoApp="showTodoApp" />
  <Todo v-if="showTodoApp" title="Todo App" />
  <Timer v-else />
</template>

<script>
import Todo from "./components/Todo.vue";
import Timer from "./components/Timer.vue";
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  data() {
    return {
      showTodoApp: true,
    };
  },
  methods: {
    toggleApp(value) {
      this.showTodoApp = value;
    },
  },
  components: {
    Todo,
    Timer,
    Navbar,
  },
};
</script>
