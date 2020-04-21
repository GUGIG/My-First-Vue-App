<template>
    <div> <!--class="clearAllContainer"-->
        <button class="clearAllBtn" @click="clearTodo">Clear All</button>
    </div>
</template>

<script>
export default {
    methods: {
        clearTodo: function() {
            this.$emit('removeAll');
        }
    }
};
</script>

<style> /* 얘는 왜 또 scoped면 적용이 안되는거임??*/
.clearAllContainer { /* button 태그를 사용했으므로 얘는 사용 안하게됨. */
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin: 0 auto;    
}
.clearAllBtn {
    background-color: white;
    color: #E20303;
    display: block;
    border: none;
    width: 8.5rem;
    height: 50px;
    margin: auto;
}
</style>