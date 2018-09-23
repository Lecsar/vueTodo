<template>
  <div id="app">
    <TopPartTodo v-bind:isAllCompleted="isAllCompleted" v-bind:add-task="addTask" v-bind:toogleAllSelect="toogleAllSelect" />

    <Tasks
    v-bind:correctedTaskId="correctedTaskId"
    v-bind:tasks="tasks"
    v-bind:deleteTask="deleteTask"
    v-bind:correctTask="correctTask"
    v-bind:chooseTaskForCorrect="chooseTaskForCorrect"
    />
  </div>
</template>

<script>
import TopPartTodo from './components/TopPartTodo.vue';
import Tasks from './components/Tasks.vue';

const NOONE_TASK_CORRECTED = -1;

export default {
  name: 'app',
  components: { TopPartTodo, Tasks },
  data() {
    return {
      lastId: 1,
      tasks: [],
      isAllCompleted: false,
      correctedTaskId: NOONE_TASK_CORRECTED
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
    },

    chooseTaskForCorrect: function(taskId) {
      this.correctedTaskId = taskId;
    },

    correctTask: function(newTaskName) {
      const { correctedTaskId } = this;

      this.tasks = this.tasks.map(task => {
        if (task.id === correctedTaskId) {
          task.name = newTaskName;
        }

        return task;
      });

      this.correctedTaskId = NOONE_TASK_CORRECTED;
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
