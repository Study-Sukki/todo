<template>
  <div id="app">
    <TodoHeader @addItem="addTodo" />
    <TodoInput />
    <TodoList :todoItemLists="todoItems" @removeTodo="removeTodo" />
    <TodoFooter @removeAll="removeAll" />
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'


export default {
  data() {
    return {
      todoItems: [] //데이터 속성 todoItems 선언
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i=0; i<localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(
            JSON.stringify(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  methods: {
    addTodo(todoItem) {
      let value = {
        item: todoItem,
        completed: false
      };
      localStorage.setItem(todoItem, JSON.stringify(value));
      this.todoItems.push(value);
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    removeAll() {
      localStorage.clear();
      this.todoItems=[];
    },
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Itim&display=swap');

body {
  font: 1.2rem 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background: #f5f5f5;
  color: #111111;
  max-width: 35rem;
  margin: 8rem auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 300;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 0.5rem 1rem 1rem rgba(0, 0, 0, 0.03);
}
</style>
