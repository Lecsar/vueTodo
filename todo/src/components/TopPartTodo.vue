<template>
    <div class="top">
        <input v-bind:checked="isAllCompleted" v-on:click="toogleAllSelect" class="top__checkbox" type="checkbox">
        <input ref="taskName" @keydown.enter="addTaskAndClearInput(value)"  @keydown.esc="clearInput" class="top__input" type="text" v-model="value">
    </div>
</template>

<script>
export default {
  name: 'TopPartTodo',
  data() {
    return {
      value: ''
    };
  },
  props: {
    isAllCompleted: Boolean,
    addTask: Function,
    toogleAllSelect: Function
  },

  methods: {
    addTaskAndClearInput: function(value) {
      const name = value.trim();

      if (name) {
        this.addTask(value);
        this.clearInput();
      }
    },

    clearInput: function() {
      this.value = '';
    }
  }
};
</script>



<style lang="less" scoped>
.top {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 55rem;
  height: 6rem;
  box-sizing: border-box;

  &__checkbox {
    width: 3rem;
    height: 3rem;
  }

  &__input {
    height: 5rem;
    width: 50rem;
    outline: none;
    border: 1px solid black;
    font-size: 2rem;
    box-sizing: border-box;
    padding-left: 1rem;
  }
}
</style>
