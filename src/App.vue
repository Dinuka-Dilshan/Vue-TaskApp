<template>
  <div class="app-bar">
    <span>Task Manager</span>
  </div>
  <AddTask @add="add" />
  <TaskCard
    v-for="task in tasks"
    :key="task.id"
    :title="task.title"
    :id="task.id"
    :isDone="task.isDone"
    @delete="remove"
    @done="done"
  />
</template>

<script>
import TaskCard from "./Components/TaskCard.vue";
import AddTask from "./Components/AddTask.vue";
export default {
  data() {
    return {
      tasks: [],
    };
  },
  components: { TaskCard, AddTask },
  methods: {
    remove(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    done(id) {
      this.tasks = this.tasks.map((task) => {
        if (task.id === id) {
          return { ...task, isDone: !task.isDone };
        } else {
          return task;
        }
      });
    },
    add(text) {
      this.tasks.unshift({ id: this.tasks.length, title: text, isDone: false });
    },
  },
};
</script>

<style>
body {
  margin: 0;
  @import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");
  font-family: "Inter", sans-serif;
}

.app-bar {
  width: 100%;
  height: 5rem;
  display: flex;
  align-items: center;
  padding: 2rem;
  box-sizing: border-box;
  font-size: 1.5rem;
  font-weight: bold;
  color: #0c2d66;
  border-bottom: 1px solid #e8e9eb;
}
</style>
