<template>
    <div class="clearAllContainer">
        <span class="clearAllBtn" v-on:click="clearTodo">
            Clear All
        </span>
    </div>
</template>

<script>
export default {
    methods: {
        clearTodo: function(){
            localStorage.clear();
            // .clear() : 로컬스토리지에 있는 모든 내용을 지우는 API
        }
    }
};
</script>

<style scoped>
.clearAllContainer {width: 8.5rem; height: 50px; line-height: 50px; border-radius: 5px; margin: 0 auto; background-color: #8763fb;}
.clearAllBtn {color: #fff; display: block;}
</style>