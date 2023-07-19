<template>
  <div id="app">
    <section class="todoapp">
      <TodoHeader @addItem="addTodo" />
      <TodoInput
        :todoCount="remainCount"
        :todoItemLists="todoItems" 
        @toggleAll="toggleAll" />
      <TodoList
        :todoItemLists="todoItems"
        @removeTodo="removeTodo"
        @toggleItem="toggleCompleted" />
      <TodoFooter
        :filterType="filterType"
        :todoCount="remainCount"
        :size="filteredList.length"
        :todoItemLists="todoItems"
        @removeAll="removeAll"
        @removeCompleted="removeCompleted"
        @onFilterType="handleFilterType" />
    </section>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data () {
    return {
      todoItems: [], //데이터 속성 todoItems 선언
      filterType: 'All' //기본 필터 All로 지정
    }
  },
  created () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(JSON.parse((localStorage.getItem(localStorage.key(i)))));
        }
      }
    }
  },
  methods: {
    addTodo (todoItem) {
      const value = {
        item: todoItem,
        completed: false
      };
      localStorage.setItem(todoItem, JSON.stringify(value));
      this.todoItems.push(value);
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
    toggleAll () {
      this.todoItems.forEach((todoItem) => todoItem.completed = event.target.checked)
    },
    removeCompleted () {
      this.todoItems = this.todoItems.filter(todoItem => {
        return !todoItem.completed
      })
    },
    handleFilterType (type) {
      this.filterType = type;
    }
  },
  computed: {
    remainCount () {
      let leftCount = 0;
      for (let i = 0; i < this.todoItems.length; i++) {
        if (this.todoItems[i].completed === false) {
          leftCount++;
        }
      }
      return leftCount;
    },
    filteredList () {
      switch (this.filterType) {
        case "All": {
          return this.todoItems
        }
        case "Active": {
          return this.todoItems.filter((todoItem) => !todoItem.completed)
        }
        case "Completed": {
          return this.todoItems.filter((todoItem) => todoItem.completed)
        }
        default: {
          return []
        }
      }
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

html,
body {
  margin: 0;
  padding: 0;
}
body {
  font: 1.2rem 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background: #f5f5f5;
  color: #4d4d4d;
  min-width: 12rem;
  max-width: 35rem;
  margin: 8rem auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 300;
}
button {
  margin: 0;
  padding: 0;
  border: 0;
  background: none;
  font-size: 100%;
  vertical-align: baseline;
  font-family: inherit;
  font-weight: inherit;
  color: inherit;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-style: groove;
}
:focus {
  outline: 0;
}
.hidden {
  display: none;
}
.todoapp {
  background: #fff;
  margin: 5rem 0 2rem 0;
  position: relative;
  box-shadow: 0 0.1rem 0.2rem 0 rgba(0, 0, 0, 0.2),0 1rem 2rem 0 rgba(0, 0, 0, 0.1);
}
.todoapp input::-webkit-input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}
.todoapp input::-moz-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}
.todoapp input::input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}
</style>
