<template>
  <div class="container">
    <h2>{{ title }}</h2>

    <div class="input__box">
      <input v-model="taskName" type="text" required="" />
      <label>Task</label>
    </div>
    <button @click="add">Add</button>

    <p v-if="tasks.length === 0" class="empty__state">No tasks yet</p>
    <ul>
      <li class="todo__container" v-for="task in tasks" v-bind:key="task.id">
        <p>{{ task.name }} &nbsp;</p>
        <p class="remove__task__button" @click="removeTask">x</p>
        <p
          @click="toggleStatus(task)"
          v-if="task.status"
          :data-status="task.status"
        >
          ✔
        </p>
        <p @click="toggleStatus(task)" v-else :data-status="task.status">✔</p>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
export default {
  name: "Todo",
  props: {
    title: String,
  },
  data() {
    return {
      tasks: [],
      taskName: "",
    };
  },
  methods: {
    add: function () {
      this.tasks.push({
        name: this.taskName,
        status: false,
        id: this.tasks.length,
      });
    },
    toggleStatus: function (task) {
      task.status = !task.status;
    },
    removeTask: function (task) {
      this.tasks.splice(this.tasks.indexOf(task), 1);
    },
  },
};
</script>

<style scoped>
.container {
  width: 400px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  position: absolute;
  padding: 40px;
  box-sizing: border-box;
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.6);
  color: white;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.5);
  text-align: left;
}

.container h2 {
  text-align: center;
}

.input__box {
  position: relative;
}

.input__box input {
  width: 100%;
  border: none;
  outline: none;
  background: transparent;
  color: white;
  font-size: 16px;
  padding: 10px 0;
  margin-bottom: 30px;
  border-bottom: 1px solid #fff;
}

.input__box label {
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 0;
  font-size: 16px;
  color: #fff;
  pointer-events: none;
  transition: 0.2s ease all;
}

.input__box input:focus ~ label,
.input__box input:valid ~ label {
  top: -18px;
  left: 0;
  color: #03a9f4;
  font-size: 12px;
  pointer-events: none;
}

.container button {
  background: transparent;
  border: none;
  outline: none;
  color: white;
  background: #03a9f4;
  padding: 10px 20px;
  width: 100%;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.2s ease all;
  left: 0%;
}

ul {
  width: 100%;
  padding: 0;
  max-height: 400px;
  overflow: auto;
  padding-right: 10px;
}

ul::-webkit-scrollbar {
  width: 10px;
}

ul::-webkit-scrollbar-track {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.8);
  border-radius: 15px;
}

ul::-webkit-scrollbar-thumb {
  border-radius: 15px;
  background-color: #03a9f4;
}

.todo__container {
  display: flex;
  align-content: center;
  justify-content: center;
  position: relative;
  margin-left: 20px;
}

.todo__container p {
  text-transform: capitalize;
  border: 1px solid #fff;
  padding: 10px;
  transition: 0.8s ease;
}

.todo__container p:first-child {
  width: 100%;
  padding-left: 20px;
}

.todo__container p:last-child[data-status="true"],
.todo__container p:last-child[data-status="false"] {
  position: absolute;
  cursor: pointer;
  left: -20px;
  top: 0;
  height: 19px;
  color: #fff;
  border-right: none;
  background: green;
}

.todo__container p:last-child[data-status="false"] {
  background: orange !important;
}

.empty__state {
  text-align: center;
  color: #fff;
  font-size: 16px;
  margin-top: 20px;
  padding: 10px;
  background: rgba(106, 119, 122, 0.432);
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.5);
}

.todo__container .remove__task__button,
.edit__task__button {
  position: absolute;
  right: 0;
  top: 0;
  cursor: pointer;
  color: #fff;
  border-left: none;
  background: red;
  padding: 10px;
  transition: 0.2s ease all;
}
</style>
