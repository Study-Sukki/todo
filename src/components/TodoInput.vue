<template>
  <div>
    <input 
      class="new-todo" 
      v-model="newTodoItem"
      @keyup.enter="addTodo"
      autofocus placeholder="What needs to be done?" />
    <section class="toggle-bar"> 
      <!-- v-show="todos.length" -->
      <input
        id="toggle-all" 
        class="toggle-all" 
        type="checkbox"
        :checked="remaining === 0"
        @:change="toggleAll" />
      <label for="toggle-all">Mark all as complete</label>
    </section>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ''
      //input에서 v-model="newTodoItem"을 통해 입력하는 값이 바로 newTodoItem 데이터로 들어감
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== '') {
        //input에 입력된 값이 빈값이 아니면 실행되도록
        let value = {
          item: this.newTodoItem,
          completed: false
        };
        localStorage.setItem(this.newTodoItem, JSON.stringify(value));
        //App컴포넌트로 이벤트 전달
        this.clearInput();
        //input초기화 > 지금 안됨... 왜 안되지
      }
      // 1. 위에서 v-model을 썼는데, input에 입력하는 값이 그대로 newTodoItem에 안들어감.. 왜그럴까요?
    },
    clearInput() {
      this.newTodoItem= '';
    },
  }
}
</script>

<style scoped>
.new-todo {
  background: #fff;
  margin: 0;
  font-size: 2rem;
  width: 100%;
  font-family: inherit;
  font-weight: inherit;
  padding: 1rem 1rem 1rem 6rem;
  height: 5rem;
  border: none;
  background: rgba(0, 0, 0, 0.003);
  position: relative;
  width: 100%;
  line-height: 1.4rem;
  color: inherit;
  box-sizing: border-box;
}
/* .new-todo:focus {
  position: relative;
  margin: 0;
  border: 0.1rem solid #999;
} */
.input::-webkit-input-placeholder {
  font-style: italic;
  font-weight: 400;
  color: rgba(0, 0, 0, 0.4);
}
.input::-moz-placeholder {
  font-style: italic;
  font-weight: 400;
  color: rgba(0, 0, 0, 0.4);
}
.input::input-placeholder {
  font-style: italic;
  font-weight: 400;
  color: rgba(0, 0, 0, 0.4);
}
.input:focus {
  outline: 0.2rem solid red;
}
.toggle-bar {
  position: relative;
  z-index: 2;
  border-top: 0.1rem solid #e6e6e6;
}
.toggle-all {
  width: 1rem;
  height: 1rem;
  border: none;
  opacity: 0;
  position: absolute;
  right: 100%;
  bottom: 100%;
}
.toggle-all + label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 4.5rem;
  height: 6.5rem;
  font-size: 0;
  position: absolute;
  top: -6.5rem;
  left: -0;
}
.toggle-all + label:before {
  content: '❯';
  display: inline-block;
  font-size: 10rem;
  color: #949494;
  padding: 1rem 1rem 1rem 1rem;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}
.toggle-all:checked + label:before {
  color: #484848;
}
</style>
