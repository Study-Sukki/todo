<template>
  <footer class="footer-end">
    <span class="todo-count">
      <strong> {{ todoCount }}</strong>
      <span>{{ todoCount === 1 ? ' item' : ' items' }} left</span>
    </span>
    <span class="clearAllBtn" type="button" @click="clearTodo">Clear All</span>
  </footer>
</template>

<script>
export default {
  props: {
    todoCount: {
      type: Number,
      required: true  
    }
  },
  methods: {
    clearTodo: function() {
      this.$emit('removeAll');
    }
  }
}
</script>

<style scoped>
.footer-end {
  padding: 1rem 1.5rem;
  border-top: 0.1rem solid #e6e6e6;
}
.clearAllBtn {
  color: #e20303;
  text-align: center;
  display: block;
}
.todo-count {
  font-size: 1rem;
}
</style>
