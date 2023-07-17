<template>
  <section class="main">
    <ul class="todo-list">
      <li v-for="(todoItem, index) in todoItemLists" :key="todoItem.item">
        <div class="view">
          <input
            class="toggle"
            type="checkbox" 
            :id="todoItem.item"
            :checked="todoItem.completed === true"
            @change="toggleCompleted(todoItem)" />
          <label :for="todoItem.item" class="list-label">
            <p class="list-text">{{ todoItem.item }}</p>
          </label>
          <button class="removeBtn" @click="removeTodo(todoItem, index)" />
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    todoItemLists: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    toggleCompleted (todoItem, index) {
      this.$emit('toggleItem', todoItem, index);
    },
    removeTodo (todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    }
  },
}
</script>

<style>
.main {
  position: relative;
  z-index: 2;
  border-top: 0.1rem solid #e6e6e6;
}
.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
.todo-list li {
  position: relative;
  font-size: 1.5rem;
  border-bottom: 0.1rem solid #ededed;
  display: flex;
  min-height: 4rem;
  margin: 0.1rem 0;
  padding: 0 0.1rem;
  background: white;
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
  line-height: 1.2;
  transition: color 0.4s;
}
.todo-list li .toggle + label {
  background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23949494%22%20stroke-width%3D%223%22/%3E%3C/svg%3E');
  background-repeat: no-repeat;
  background-position: center left;
}
.todo-list li .toggle:checked + label {
  background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%2359A193%22%20stroke-width%3D%223%22%2F%3E%3Cpath%20fill%3D%22%233EA390%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22%2F%3E%3C%2Fsvg%3E');
}
.todo-list input:checked+label .list-text{
  color: #cc9a9a;
  text-decoration: line-through;  
}
.todo-list li .removeBtn {
  display: none;
  position: absolute;
  top: 0;
  right: 0.2rem;
  bottom: 0.2rem;
  width: 3rem;
  margin: auto 0;
  color: #cc9a9a;
  transition: color 0.2s ease-out;
}
.todo-list li .removeBtn:hover {
  color: #af5b5e;
}
.todo-list li .removeBtn:after {
  content: "x";
  height: 100%;
}
.todo-list li:hover .removeBtn {
  display: block;
}
.list-text {
  margin: 1rem 0 1rem 3rem;
}
</style>
