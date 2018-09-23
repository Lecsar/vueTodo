<template>
    <ul class="list">
        <li class="list__task" v-bind:key="task.id" v-for="task in tasks">
          <input v-if="task.id !== correctedTaskId" v-model="task.isCompleted" class="list__task__checkbox" type="checkbox" >
          <span
          class="list__task__name"
          v-if="task.id !== correctedTaskId"
          v-on:dblclick="chooseTaskForCorrect(task.id)"
          >
            {{task.name}}
          </span>
          <span v-if="task.id !== correctedTaskId" v-on:click="deleteTask(task.id)" class="list__task__delete">&times;</span>
          
          <input
          autofocus
          v-else
          class="list__changed-name"
          type="text"
          v-model="inputValue"
          @keydown.esc="clearInput"
          @keydown.enter="correctOrDeleteTask" />
        </li>
    </ul>
</template>

<script>
export default {
  name: 'Tasks',
  props: {
    correctedTaskId: Number,
    tasks: Array,
    deleteTask: Function,
    correctTask: Function,
    chooseTaskForCorrect: Function
  },

  data() {
    return {
      inputValue: ''
    };
  },

  methods: {
    correctOrDeleteTask: function() {
      const name = this.inputValue.trim();

      if (name) {
        this.correctTask(name);
      } else {
        this.deleteTask(this.correctedTaskId);
      }
    },

    clearInput: function() {
      this.inputValue = '';
    }
  }
};
</script>

<style lang="less" scoped>
.list {
  min-width: 55rem;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  margin-top: 2rem;

  &__task {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin: 0.5rem 0;
    list-style-type: none;
    font-size: 3rem;

    &__checkbox {
      width: 3rem;
      height: 3rem;
      cursor: pointer;
    }

    &__name {
      width: 45rem;
      cursor: pointer;
    }

    &__delete {
      cursor: pointer;
      color: rgb(253, 78, 78);

      &:hover {
        color: rgb(196, 6, 6);
      }
    }
  }

  &__changed-name {
    margin-left: 5rem;
    height: 4rem;
    width: 100%;
    box-sizing: border-box;
    outline: none;
    font-size: 2.5rem;
    padding-left: 1rem;
    border: 1px solid blue;

    &:focus {
      border-color: black;
    }
  }
}
</style>
