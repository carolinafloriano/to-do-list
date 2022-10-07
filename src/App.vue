<template>
  <div id="app">
    <div class="todo-list">
      <h1 class="title">To-do List</h1>
      <p>{{ completedTasks }} / {{ totalTasks }} Concluded</p>
      <form @submit.prevent="setNewTask">
        <input
          v-model="nameTask"
          class="input-text"
          type="text"
          placeholder="Insert a new task"
        />
        <button class="button">New</button>
      </form>
      <ul>
        <li v-for="(item, index) in tasks" :key="'task' + index">
          <input type="checkbox" v-model="item.completed" />
          <label>{{ item.name }}</label>
          <button class="deleteButton" @click="deleteTask(index)">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      nameTask: "",
      tasks: [
        {
          name: "Mindmap",
          completed: true,
        },
        {
          name: "Wireframe",
          completed: false,
        },
      ],
    };
  },

  methods: {
    setNewTask() {
      this.tasks.push({ name: this.nameTask, completed: false });
      this.nameTask = "";
    },
    deleteTask(index) {
      console.log(index);
      this.tasks.splice(index, 1);
    },
  },

  computed: {
    totalTasks: function () {
      return this.tasks.length;
    },
    completedTasks: function () {
      var completed = 0;

      for (const item of this.tasks) {
        if (item.completed) {
          completed = completed + 1;
        }
      }
      return completed;
    },
  },
};
</script>

<style>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css";

body {
  background-color: #f0f8ff;
  margin: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}

.todo-list {
  box-sizing: border-box;
  background-color: #ffffff;
  width: 35%;
  height: 70%;
  border-radius: 5px;
  box-shadow: 0 0 10px #bebebe;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.title {
  font-size: 1.5em;
}

.input-text {
  box-sizing: border-box;
  box-shadow: 0px 2px 5px rgb(132, 131, 131);
  border-radius: 5px;
  border: 1px solid #ffffff;
  line-height: 2em;
  margin: 0.6em;
  color: #413f3f;
  outline: none;
}

.input-text:focus {
  border: 2px solid #1e90ff;
}

.input-text::placeholder {
  color: #bebebe;
  padding: 1.5px;
}

input:checked + label {
  text-decoration: line-through;
}

.button {
  color: #ffffff;
  background-color: #1e90ff;
  font-size: 1em;
  font-weight: bold;
  padding: 7px 20px;
  border-width: 0;
  border-radius: 5px;
  box-shadow: 0px 2px 5px rgb(132, 131, 131);
}

.deleteButton {
  background-color: rgb(214, 4, 4);
  color: #ffffff;
  border-radius: 5px;
  border: 0;
  width: 25px;
  aspect-ratio: 1;
}

li {
  width: 100%;
  list-style: none;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 5px;
}

@media (max-width: 600px) {
  .todo-list {
    width: 90%;
    height: 50%;
  }
}
</style>
