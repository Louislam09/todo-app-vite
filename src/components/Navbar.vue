<template>
  <nav>
    <ul>
      <li @click="showTodoApp(true)" :data-s="sTodoApp">Todo</li>
      <li @click="showTodoApp(false)" :data-s="!sTodoApp">Timer</li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    sTodoApp: Boolean,
  },
  methods: {
    showTodoApp(value) {
      this.$emit("toggleTodoApp", value);
    },
  },
};
</script>

<style scoped>
nav {
  position: relative;
  font-family: "Poppins", sans-serif;
  width: 100%;
  height: 3rem;
  background: rgba(15, 21, 31, 0.8);
  padding: 0px 20px;
}

nav ul {
  display: flex;
  justify-items: center;
  justify-content: end;
  height: 100%;
}

nav ul li {
  position: relative;
  padding: 5px 0px;
  list-style: none;
  font-size: 1.5rem;
  color: white;
  margin: 0 10px;
  cursor: pointer;
  transition: all 3s ease;
}

nav ul li[data-s="true"]::after {
  content: "";
  position: absolute;
  width: 80%;
  height: 2px;
  background: #ffc107;
  bottom: 10px;
  left: 0;
  transition: all 0.3s ease-in-out;
  animation: grow 0.8s ease;
}

@keyframes grow {
  0% {
    width: 0%;
  }
  100% {
    width: 80%;
  }
}
</style>















