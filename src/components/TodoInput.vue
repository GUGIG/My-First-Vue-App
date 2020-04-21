<template>
    <div class="inputBox shadow">
        <!-- <div>
            {{ newTodoItem }}
        </div>-->
        <input
            type="text"
            v-model="newTodoItem"
            placeholder="Type what you have to do"
            @keydown.enter.exact="addTodo"
        />
        <!-- 
            form관련 태그 실시간 데이터 바인딩. 
            책에선 span을 썼지만, button이면 button을 쓰는게 바람직하단다.
        -->
        <button class="addContainer" @click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
            <!-- using awesome icon -->
        </button>

        <Modal v-if="showModal" @close="showModal = false" class="modal">
            <h3 slot="header">경고</h3>
            <div slot="body"></div> <!--defalut body 메세지 안띄우려고 빈 div태그에 slot 넣음. -->
            <span slot="footer" @click="showModal = false">
                할 일을 입력하세요!
                <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
            </span>
        </Modal>
    </div>
</template>

<script>
import Modal from "./common/Modal.vue";

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false
        };
    },
    methods: {
        addTodo: function() {
            if (this.newTodoItem !== "") {
                // 값이 있을 때만 밑의 로직 실행
                var value = this.newTodoItem && this.newTodoItem.trim(); // 뭔데 이거;;
                this.$emit("addTodo", value);
                this.clearInput();
            } else {
                // alert("값을 입력하세요!");
                this.showModal = !this.showModal;
            }
        },
        clearInput: function() {
            this.newTodoItem = "";
        }
    },
    components: {
        Modal: Modal
    }
};
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    /* display: inline-block; float: right 때문에 그냥 block이 되버려서 얘는 무시된단다.*/
    width: 3rem;
    height: 50px;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
</style>