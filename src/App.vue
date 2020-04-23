<template>
    <div id="app">
        <TodoHeader></TodoHeader>
        <TodoInput @addTodo="addTodo"></TodoInput>
        <TodoList :propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
        <TodoFooter @removeAll="clearAll"></TodoFooter>
    </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
//testing
export default {            
    data() {
        return {
            todoItems: []
        }
    },
    methods: {
        addTodo: function(todoItem) {
            localStorage.setItem(todoItem, todoItem);
            this.todoItems.push(todoItem);
        },
        clearAll: function() {
            localStorage.clear();
            this.todoItems = []; // gc?
        },
        removeTodo: function(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        }
    },
    created() {
        if (localStorage.length > 0) {
            for (let i = 0; i < localStorage.length; i++) {
                if (localStorage.key(i) != "loglevel:webpack-dev-server") {
                    console.log(
                        `localStorage.key(${i}) >> `,
                        localStorage.key(i)
                    ); // 왜 순서가 뒤죽박죽일까?
                    this.todoItems.push(localStorage.key(i));
                }
            }
        }
    },
    components: {
        TodoHeader: TodoHeader,
        TodoInput: TodoInput,
        TodoList: TodoList,
        TodoFooter: TodoFooter
    },
};
</script>

<style>
body {
    text-align: center;
    background-color: #F6F6F8;
}
input {
    border-style: groove;
    width: 200px;
    text-align: center;
}
button {
    border-style: groove;
}
.shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
