<template>
    <div>
        <input type="text" v-model="newTodoItem" /> <!-- form관련 태그 실시간 데이터 바인딩. -->
        <button @click="addTodo">추가</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTodoItem: ''
        };
    },
    methods: {
        addTodo: function() {
            if(this.newTodoItem !== '') {
                var value = this.newTodoItem && this.newTodoItem.trim(); // 뭔데 이거;;
                localStorage.setItem(value, value);
                this.clearInput();
            }            
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    }
};
</script>

<style>
</style>