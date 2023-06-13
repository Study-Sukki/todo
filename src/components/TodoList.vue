<template>
    <div>
        <ul class="todo-list">
            <li
                v-for="todoItem in propsdata" 
                class="todo"
                v-bind:key="todoItem">
                <div class="view">
                    <input class="toggle" type="checkbox">
                    <label> {{ todoItem }} </label>
                    <button class="removeBtn" v-on:click="removeTodo(todoItem, index)"></button>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    created(){
        if(localStorage.length > 0){
            for(var i= 0; i< localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    props: ['propsdata'],
    methods: {
        removeTodo(todoItem, index) {
            this.$emit('removeTodo', todoItem, index);
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index,1); 
            //특정 index에서 하나만 지울 수 있는 기능
        }
    },
}
</script>

<style>
li{
    display: flex;
    min-height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.todo-list li .removeBtn {
    position: absolute;
    border: none;
    background-color: inherit;
	margin: auto 0;
	font-size: 30px;
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