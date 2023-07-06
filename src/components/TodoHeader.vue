<template>
  <header>
    <h1>todos</h1>
      <input 
        class="new-todo" 
        v-model="newTodoItem"
        @keyup.enter="addTodo"
        placeholder="What needs to be done?" />
        {{ todoItem }}
  </header>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ''
      //input에서 v-model="newTodoItem"을 통해 입력하는 값이 바로 newTodoItem 데이터로 들어감
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        this.$emit("addItem", this.newTodoItem);
        this.clearInput();
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  }
}
</script>

<style>
h1 {
  position: absolute;
  top: -5rem;
  width: 100%;
  font-size: 7rem;
  font-weight: 200;
  text-align: center;
  color: #b83f45;
  max-width: 35rem;
}
.new-todo {
  margin: 0;
  font-size: 1.7rem;
  width: 100%;
  font-family: inherit;
  font-weight: inherit;
  padding: 1rem 1rem 1rem 4rem;
  height: 5rem;
  border: none;
  position: relative;
  width: 100%;
  line-height: 1.4rem;
  color: inherit;
  box-sizing: border-box;
  box-shadow: 0.5rem 1rem 1rem rgba(0, 0, 0, 0.1);
}
</style>
