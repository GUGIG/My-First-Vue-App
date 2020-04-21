<template>
    <section>
        <!-- ul>li{할 일 $}*4 -->
        <transition-group name="list" tag="ul"> <!--여기서 name속성은 form에서의 name과는 다르다. 이놈에게 적용할 css와 관련이 있다고 한다. -->
            <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
                <!-- 책에선 v-for할 때 :key를 꼭 넣어주는게 '좋다' 라고 되어있다. 나중에 버전이 올라가면서 이건 필수가 된 것 같다. -->
                <i class="checkBtn fa fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                <span
                    class="removeBtn"
                    type="button"
                    @click="removeTodo(todoItem, index)"
                >
                    <i class="fa fa-trash-o" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>

<script>
export default {
    props: ["propsdata"], // 얘는 data옵션처럼 함수로 선언 안해도 되는거야...?
    methods: {
        removeTodo: function(todoItem, index) {
            // localStorage.removeItem(todoItem);
            // this.propsdata.splice(index, 1); 만약 이벤트 활성 대신 얘를 썼어도 정상작동할까?
            this.$emit("removeTodo", todoItem, index);
        }
    }
};
</script>

<style>
/* 얘는 왜 scope를 안할까..? 일단 이해 안되는건 얘는 scoped하면 작동 안함.*/
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}
.removeBtn {
    margin-left: auto;
    color: #de4343;
}

.list-item {
    display: inline-block;
    margin-right: 10px;
}
.list-move {
    transition: transform 1s; /* 얘는 없어도 동작하던데, 왜있는거임? */
}
.list-leave-active { /* li 하나 없어질 때 바뀌어야할 style & delay time */
    /* transition: opacity .3s, transform .5s; */
    transition: background-color .2s, transform .4s;
}
.list-enter-active { /* li 추가될 때 바뀌어야할 style & delay time */
    transition: transform .3s;
}
.list-leave-to { /* li 없어질 때 동작해야할 애니메이션 */
    /* opacity: 0; */
    transform: translateX(100%);
    background-color: aquamarine;
}
.list-enter { /* li 추가될 때 동작해야할 애니메이션 */
    transform: translateX(100%);
}
</style>