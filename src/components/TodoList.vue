<template>
  <div>
    <ul class="todo-list">
      <li
        v-for="todoItem in todoItemList" 
        class="todo"
        :key="todoItem.item">
        <div>
          <input 
          class="toggle"
          type="checkbox"
          :id="todoItem.item"
          :checked="todoItem.completed === true"
          @change="toggleComplete(todoItem)" />
          <label :for="todoItem.item" class="list-label"> {{ todoItem.item }} </label>
          <button class="removeBtn" @click="removeTodo(todoItem, index)" />
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['todoItemList'],
  methods: {
    toggleComplete(todoItem) {
    todoItem.completed = !todoItem.completed;
    localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
  }
}
</script>

<style>
li {
  display: flex;
  min-height: 50rem;
  line-height: 50rem;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5rem;
}
.todo-list li .removeBtn {
  position: absolute;
  border: none;
  background-color: inherit;
  margin: auto 0;
  font-size: 30rem;
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
</style>
