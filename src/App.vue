<template>
  <div id="app">
    <TodoHeader @addItem="addTodo" />
    <TodoInput @toggleAll="toggleAll"/>
    <TodoList 
      :todoItemLists="todoItems" 
      @removeTodo="removeTodo" 
      @toggleItem="toggleCompleted"/>
    <TodoFooter @removeAll="removeAll" :todoCount="remaining"/>
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
      todoItems: [], //데이터 속성 todoItems 선언
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(
            JSON.stringify(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  methods: {
    addTodo (todoItem) {
      let value = {
        item: todoItem,
        completed: false
      };
      localStorage.setItem(todoItem, JSON.stringify(value));
      this.todoItems.push(value);
    },
    toggleAll (todo) {
      this.todoItems.forEach((todoItem) => (todoItem.completed = todo.todoItems.checked))
    },
    removeTodo (todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleCompleted (todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    removeAll () {
      localStorage.clear();
      this.todoItems=[];
    },
  },
  computed: {
    remaining () {
      let leftCount = 0;
      for (let i = 0; i < this.todoItems.length; i++) {
        if (this.todoItems[i].completed === false) {
          leftCount++;
        }
      }
      return leftCount;
    }
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
