<template>
  <div>
    <section v-show="todoItemLists.length">
      <input
        id="toggle-all" 
        class="toggle-all"
        type="checkbox"
        @change="toggleAll"
        :checked="todoCount === 0" />
      <label for="toggle-all">Mark all as complete</label>
    </section>
  </div>
</template>

<script>
export default {
  props: {
  todoCount: {
    type: Number,
    required: true  
    },
  todoItemLists: {
    type: Array,
    default: () => []
    }
  },
  methods: {
    toggleAll () {
        this.$emit('toggleAll');
    },
  }
}
</script>

<style scoped>
/* toggle-all label은 클릭하기 전에는 보이면 안되고, 클릭했을때만 보이게 해야함 */
/* toggle-all을 포함하고 있는 네모칸도 클릭했을때 주변 테두리 들어갈 수 있도록 하기*/
.toggle-all {
  width: 0.1rem;
  height: 1rem;
  opacity: 0;
  position: absolute;
  border: none;
  right: 100%;
  bottom: 100%;
}
.toggle-all + label{
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 3rem;
  font-size: 0;
  top: 1rem;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}
.toggle-all + label:before {
  content: '❯';
  display: inline-block;
  font-size: 2rem;
  color: #e6e6e6;
  padding: 0 1rem 0 1rem;
}
.toggle-all:checked + label:before {
  color: #d91111;
}
.toggle-all {
  display: none;
}
</style>
