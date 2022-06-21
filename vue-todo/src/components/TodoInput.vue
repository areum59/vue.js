<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <!-- v-model : 입력 값을 vue인스턴스에 즉각 맵핑 -->
        <button class="addContainer" v-on:click="addTodo">
            <font-awesome-icon icon="fas fa-plus" />
        </button>
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
            if(this.newTodoItem !== ''){
                this.$emit('addTodoItem', this.newTodoItem);
                // this.$emit('event-name', 인자1, 인자2, ....);
                this.clearInput();
            }
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
.addContainer svg {height: 1.5rem;}
</style>