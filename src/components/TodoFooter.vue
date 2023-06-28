<template>
  <footer class="footer-end">
    <span class="clearAllBtn" type="button" @click="clearTodo">Clear All
    </span>
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
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color:white;
  border-radius: 5px;
  margin: 0 auto;
}
.clearAllBtn {
  color: #e20303;
  display: block;
}
</style>
