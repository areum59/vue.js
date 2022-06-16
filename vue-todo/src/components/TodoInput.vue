<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <button class="addContainer" v-on:click="addTodo">add</button>
    </div>
</template>

<script>
export default {
    name: 'VueTodoInput',

    data: function() {
        return {
            newTodoItem: ""
        };
    },

    methods: {
        addTodo: function(){
            // console.log(this.newTodoItem);
            // 저장하는 로직
            // localStorage.setItem(key,value);
            localStorage.setItem(this.newTodoItem,this.newTodoItem);
            this.clearInput();
        },
        clearInput: function(){
            this.newTodoItem = '';
        }
    }
};
</script>

<style scoped>
.inputBox {background-color: white; height: 50px; border-radius: 5px;}
.inputBox input {width: 80%; line-height: 48px; border-style: none; font-size: 0.9rem;}
.inputBox input:focus {outline: none;}

.addContainer {color: white; float: right; background: linear-gradient(to right, #6478fb, #8763fb); display: block; width: 3rem; height: 100%; border: none; border-radius: 0 5px 5px 0; cursor: pointer;}
</style>