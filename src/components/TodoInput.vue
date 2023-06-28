<template>
  <div>
    <input 
        class="new-todo" 
        v-model="newTodoItem"
        @keyup.enter="addTodo"
        autofocus placeholder="What needs to be done?">
    <section class="toggle-bar"> 
        <!-- v-show="todos.length" -->
        <input
            id="toggle-all" 
            class="toggle-all" 
            type="checkbox"
            :checked="remaining === 0"
            @:change="toggleAll">
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
                var value = {
                  item: this.newTodoItem,
                  completed: false
                };
                localStorage.setItem(this.newTodoItem, JSON.stringify(value));
                //App컴포넌트로 이벤트 전달
                this.clearInput();
                //input초기화 > 지금 안됨... 왜 안되지
            }
            // 1. 여기서 
        },
        clearInput() {
            this.newTodoItem= '';
            // console.log(this.newTodoItem);
            // //저장하는 로직
            // localStorage.setItem(this.newTodoItem, this.newTodoItem);
            // this.newTodoItem=""; //비워주기(초기화)
        },
    }
}
</script>

<style scoped>
.new-todo {
    background: #fff;
    margin: 130px 0 40px 0;
    position: relative;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}
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
    outline: 2px solid red;
}
.new-todo,
.edit {
    position: relative;
    margin: 0;
    width: 100%;
    font-size: 24px;
    font-family: inherit;
    font-weight: inherit;
    line-height: 1.4em;
    color: inherit;
    border: 1px solid #999;
    box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
    box-sizing: border-box;
}
.new-todo {
    padding: 16px 16px 16px 60px;
    height: 65px;
    border: none;
    background: rgba(0, 0, 0, 0.003);
    box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}
.toggle-bar {
	position: relative;
	z-index: 2;
	border-top: 1px solid #e6e6e6;
}
.toggle-all {
	width: 1px;
	height: 1px;
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
	width: 45px;
	height: 65px;
	font-size: 0;
	position: absolute;
	top: -65px;
	left: -0;
}
.toggle-all + label:before {
	content: '❯';
	display: inline-block;
	font-size: 22px;
	color: #949494;
	padding: 10px 27px 10px 27px;
	-webkit-transform: rotate(90deg);
	transform: rotate(90deg);
}
.toggle-all:checked + label:before {
	color: #484848;
}
</style>