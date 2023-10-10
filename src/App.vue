<template>
  <div id="app">
    <div class="container">
      <header>
        <h1>Tasks {{ count }}</h1>
      </header>

      <section class="Tasks">
        <div class="addTask">
          <input type="text" placeholder="New task" v-model="newTask" />
          <button @click="addTask(newTask)">
            <i class="fa-solid fa-plus"></i>Add
          </button>
        </div>

        <div class="clearButton">
          <button @click="clearComplete()">Clear Complete</button>
          <button @click="clearAll()">Clear All</button>
        </div>
      </section>

      <section class="showTask" v-for="(item, index) in tasks" :key="index">
        <div class="showTask-area" v-if="item.status == true">
          <p @click="updateStatus(item)" class="finishTask">{{ item.name }}</p>
          <button @click="deleteTask(item)">
            <i class="fa-solid fa-x"></i>
          </button>
        </div>
        <div class="showTask-area" v-else>
          <p @click="updateStatus(item)" class="notfinishTask">
            {{ item.name }}
          </p>
          <button @click="deleteTask(item)">
            <i class="fa-solid fa-x"></i>
          </button>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { remove } from "@vue/shared";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      newTask: "",
      count: 2,
      tasks: [
        {
          name: "Make todo list",
          status: true,
        },
        {
          name: "Go Skydiving",
          status: false,
        },
      ],
    };
  },
  methods: {
    addTask: function (newTask) {
      this.tasks.push({
        name: newTask,
        status: false,
      });
      this.newTask = "";
      this.count = this.countTasks();
    },
    clearComplete: function () {
      this.tasks = this.tasks.filter((task) => task.status === false);
    },
    deleteTask: function (item) {
      this.tasks = this.tasks.filter((task) => task != item);
    },
    clearAll: function () {
      this.tasks = [];
      this.count = 0;
    },
    updateStatus: function (item) {
      for (let i = 0; i < this.tasks.length; i++) {
        if (item.name == this.tasks[i].name) {
          this.tasks[i].status = !item.status;
        }
      }
      this.count = this.countTasks();
    },
    countTasks() {
      var num = 0;
      for (let i = 0; i < this.tasks.length; i++) {
        if (this.tasks[i].status === false) {
          num += 1;
        }
      }
      return num;
    },
  },
};
</script>

<style scoped>
#app {
  background: cornflowerblue;
  align-items: center;
  display: flex;
  justify-content: center;
}
.container {
  width: 50%;
  background: #fff;
  margin: 20px;
  padding: 20px;
}
header h1 {
  padding: 0;
  margin: 0;
}
.addTask {
  padding: 20px 0;
  text-align: center;
}
.addTask input {
  width: 80%;
}
.addTask button {
  width: 15%;
}
.showTask .showTask-area {
  background: rebeccapurple;
  display: flex;
  flex-direction: row;
  background: lightgray;
  margin-top: 10px;
}

.showTask .showTask-area p {
  width: 90%;
  margin: 0;
  padding: 5px;
}
.showTask .showTask-area button {
  width: 10%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.finishTask {
  text-decoration: line-through;
  background: lightgreen;
}
.notfinishTask {
  text-decoration: none;
}
</style>
