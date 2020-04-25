<template>
    <div id="app">
        <TodoHeader></TodoHeader>
        <TodoInput @addTodo="addTodo"></TodoInput>
        <TodoList :propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
        <TodoFooter @removeAll="clearAll"></TodoFooter>
        <Modal v-if="showModal" @close="showModal = false" class="modal">
            <h3 slot="header">경고</h3>
            <div slot="body"></div>
            <!--defalut body 메세지 안띄우려고 빈 div태그에 slot 넣음. -->
            <span slot="footer" @click="showModal = false">
                {{ modalMessage }}
                <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
            </span>
        </Modal>
    </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
import Modal from "./components/common/Modal.vue";
//testing
export default {
    data() {
        return {
            todoItems: [],
            modalMessage: "",
            showModal: false
        };
    },
    methods: {
        addTodo: function(todoItem) {
            if (todoItem !== "") {
                // 텅 빈 입력이 아닐 때
                var item = this.todoItems.filter(ti => ti == todoItem);
                if (item.length > 0) {
                    // 겹치는 목록이 존재할 경우
                    this.modalMessage = "이미 있는 목록입니다!";
                    this.showModal = !this.showModal;
                } else {
                    // 겹치는게 없을 경우
                    localStorage.setItem(todoItem, todoItem);
                    this.todoItems.push(todoItem);
                }
            } else {
                // 텅 빈 입력일 때
                this.modalMessage = "값을 입력하세요!";
                this.showModal = !this.showModal;
            }
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
                    this.todoItems.push(localStorage.key(i)); // 순서 뒤죽박죽으로 들어감.
                }
            }
        }
    },
    components: {
        TodoHeader: TodoHeader,
        TodoInput: TodoInput,
        TodoList: TodoList,
        TodoFooter: TodoFooter,
        Modal: Modal
    }
};
</script>

<style>
body {
    text-align: center;
    background-color: #f6f6f8;
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
