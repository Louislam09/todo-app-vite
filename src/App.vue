<template>
  <Navbar
    v-on:toggleShowAppNumber="toggleApp($event)"
    :currentAppNumber="showAppNumber"
  />
  <Todo v-show="showAppNumber === 0" title="Todo App" />
  <Timer v-show="showAppNumber === 1" />
  <Calendar v-if="showAppNumber === 2" />
  <wa-me v-if="showAppNumber === 3" title="WaMe" />
</template>

<script>
import Todo from "./components/Todo.vue";
import Timer from "./components/Timer.vue";
import Calendar from "./components/Calendar.vue";
import Navbar from "./components/Navbar.vue";
import WaMe from "./components/WaMe.vue";

export default {
  name: "App",
  data() {
    return {
      showAppNumber: Math.floor(Math.random() * 3),
    };
  },
  methods: {
    toggleApp(value) {
      this.showAppNumber = value;
    },
  },
  components: {
    Todo,
    Timer,
    Navbar,
    Calendar,
    WaMe,
  },
};
</script>

<style>
.modal {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
  transition: opacity 0.3s ease;
}
</style>
