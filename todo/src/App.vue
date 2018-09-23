<template>
  <div id="app">
    <TopPartTodo v-bind:isAllCompleted="isAllCompleted" v-bind:add-task="addTask" v-bind:toogleAllSelect="toogleAllSelect" />

    <Tasks v-bind:tasks="tasks" v-bind:deleteTask="deleteTask" />
  </div>
</template>

<script>
import TopPartTodo from './components/TopPartTodo.vue';
import Tasks from './components/Tasks.vue';
import Vue from 'vue';

export default {
  name: 'app',
  components: { TopPartTodo, Tasks },
  data() {
    return {
      lastId: 1,
      tasks: [],
      isAllCompleted: false
    };
  },

  methods: {
    addTask: function(name) {
      this.tasks.push({
        id: this.lastId,
        name,
        isCompleted: false
      });

      this.lastId++;
    },

    deleteTask: function(deletedTaskId) {
      this.tasks = this.tasks.filter(({ id }) => deletedTaskId !== id);
    },

    toogleAllSelect: function() {
      this.isAllCompleted = !this.isAllCompleted;

      this.tasks = this.tasks.map(task => {
        task.isCompleted = this.isAllCompleted;

        return task;
      });
    }
  }
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
</style>
