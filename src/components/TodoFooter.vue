<template>
  <footer class="footer-end" v-show="todoItemLists.length">
    <span class="todo-count">
      <strong>{{ todoCount }}</strong>
      <span>{{ todoCount === 1 ? ' item' : ' items' }} left</span>
    </span>
    <ul class="filters">
      <li 
        v-for="(filter, index) in filters" 
        :key="index"
        @click="handleFilterType(filter)">
        <a href="javascript:;" :class="{selected: filterType === filter}">{{ filter }}</a>
      </li>
    </ul>
    <button class="clear-completed" @click="delcompleted" v-show="todoItemLists.length>todoCount"> Clear completed </button>
    <span class="clearAllBtn" type="button" @click="clearTodo">Clear All</span>
  </footer>
</template>

<script>
export default {
  props: {
    filterType: {
      type: String,
      dafault: 'All'
    },
    todoCount: {
      type: Number,
      default: 0
    },
    todoItemLists: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      filters: ["All", "Active", "Completed"]
    }
  },
  methods: {
    clearTodo () {
      this.$emit('removeAll');
    },
    delcompleted () {
      this.$emit('removeCompleted');
    },
    handleFilterType (type) {
      this.$emit('onFilterType', type)
    }
  }
}
</script>

<style scoped>
.footer-end {
  color: #777;
  padding: 0.5rem 1rem;
  height: 2.5rem;
  text-align: center;
  font-size: 1rem;
  border-top: 0.1rem solid #e6e6e6;
}
.footer-end:before {
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  height: 1.5rem;
  overflow: hidden;
}
.clearAllBtn {
  margin: 1.5rem 0 0 0;
  color: #e20303;
  text-align: center;
  display: block;
  position: relative;
}
.todo-count {
  float: left;
  text-align: left;
}
.todo-count strong {
  font-weight: 300;
}
.filters {
  margin: 0;
  padding: 0;
  list-style: none;
  position: absolute;
  right: 0;
  left: -1rem;
}
.filters li {
  display: inline;
  margin: -0.5rem;
}
.filtered button {
  color: inherit;
  margin: 0.5rem;
  text-decoration: none;
  padding: 0.1rem 0.3rem;
  border: 0.01rem solid transparent;
  border-radius: 0.2rem;
}
.filters li a {
  color: inherit;
  margin: 0.7rem;
  text-decoration: none;
  padding: 0.1rem 0.3rem;
  border-radius: 0.2rem;
}
.filters li a:hover {
  border: 0.05rem solid #CE4646;
}
.filters li a.selected {
  border: 0.08rem solid #CE4646;
}
.clear-completed,
html, .clear-completed:active {
  float: right;
  right: -0.3rem;
  position: relative;
  line-height: 1.1rem;
  text-decoration: none;
  cursor: pointer;
}
.clear-completed:hover {
  text-decoration: underline;
}
</style>
