<template>
  <div>
    <ul class="todo-list">
      <li
        class="todoItem"
        v-for="todoItem in todoItemLists"
        :key="todoItem.item"
        >
      <input
        class="toggle"
        type="checkbox" 
        :id="todoItem.item"
        :checked="todoItem.completed === true"
        @change="toggleCompleted(todoItem)"
      />
      <label :for="todoItem.item" class="list-label">
        <p class="list-text">{{ todoItem.item }}</p>
      </label>
      <button class="removeBtn" @click="removeTodo(todoItem, index)"> </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todoItemLists: {
      type: Array,
      required: true
    }
  },
  methods: {
    toggleCompleted (todoItem) {
      this.$emit('toggleItem', todoItem);
    },
    removeTodo (todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    },
  },
}
</script>

<style>
li {
  display: flex;
  min-height: 5rem;
  line-height: 1.7rem;
  margin: 0.1rem 0;
  padding: 0 0.1rem;
  background: white;
}
.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
.todo-list li {
  position: relative;
  font-size: 1.7rem;
  border-bottom: 0.1rem solid #ededed;
  align-items: center;
}
.todo-list li:last-child {
  border-bottom: none;
}
.todo-list li .toggle {
  text-align: center;
  width: 3rem;
  height: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  border: none;
  appearance: none;
}
.todo-list li .toggle {
  opacity: 0;
}
.todo-list li label{
  word-break: break-all;
  font-size: 1.7rem;
  display: block;
  transition: color 0.4s;
  font-weight: 400;
  color: #484848;
}
.todo-list li .toggle + label {
  background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23949494%22%20stroke-width%3D%223%22/%3E%3C/svg%3E');
  background-repeat: no-repeat;
  background-position: center left;
}
.todo-list li .toggle:checked + label {
  background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%2359A193%22%20stroke-width%3D%223%22%2F%3E%3Cpath%20fill%3D%22%233EA390%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22%2F%3E%3C%2Fsvg%3E');
}
.todo-list li .removeBtn {
  position: absolute;
  border: none;
  right: 2rem;
  background-color: inherit;
  margin: auto 0;
  font-size: 1.7rem;
  color: #949494;
  transition: color 0.2s ease-out;
}
.todo-list li .removeBtn:hover,
.todo-list li .removeBtn:focus {
  color: #C18585;
}    
.todo-list li .removeBtn:after {
  content: '×';
  display: block;
  height: 100%;
  line-height: 1.1;
}
.list-text {
  margin: 1rem 0 1rem 3rem;
}
</style>
