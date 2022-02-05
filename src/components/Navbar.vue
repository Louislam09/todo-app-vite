<template>
  <nav>
    <ul>
      <li
        v-for="tab in tabs"
        :key="tab.id"
        @click="showAppNumber(tab.id)"
        :data-s="currentAppNumber === tab.id"
      >
        {{ tab.title }}
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    currentAppNumber: Number,
  },
  methods: {
    showAppNumber(value) {
      this.$emit("toggleShowAppNumber", value);
    },
  },
  data() {
    return {
      tabs: [
        {
          id: 0,
          title: "Todo",
        },
        {
          id: 1,
          title: "Timer",
        },
        {
          id: 2,
          title: "Calendar",
        },
      ],
    };
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















