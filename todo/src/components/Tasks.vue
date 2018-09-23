<template>
    <ul class="list">
        <li class="list__task" v-bind:key="task.id" v-for="task in tasks">
            <input v-model="task.isCompleted" class="list__task__checkbox" type="checkbox" >
            <span class="list__task__name">{{task.name}}</span>
            <span v-on:click="deleteTask(task.id)" class="list__task__delete">&times;</span>
        </li>
    </ul>
</template>

<script>
export default {
  name: 'Tasks',
  props: {
    tasks: Array,
    deleteTask: Function
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
}
</style>
