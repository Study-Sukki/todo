<template>
  <footer class="footer-end">
    <span class="clearAllBtn" type="button" @click="clearTodo">Clear All</span>
  </footer>
</template>

<script>
export default {
  methods: {
    clearTodo: function() {
      this.$emit('removeAll');
    }
  }
}
</script>

<style scoped>
.footer-end {
  width: 5rem;
  height: 1.5rem;
  line-height: 1.5rem;
  background-color:white;
  border-radius: 0.5rem;
  margin: 0 auto;
}
.clearAllBtn {
  color: #e20303;
  display: block;
}
</style>
