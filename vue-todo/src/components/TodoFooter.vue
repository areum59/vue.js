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
            this.$emit('clearAll');
        }
    }
};
</script>

<style scoped>
.clearAllContainer {width: 8.5rem; height: 50px; line-height: 50px; border-radius: 5px; margin: 0 auto; background-color: #8763fb;}
.clearAllBtn {color: #fff; display: block;}
</style>