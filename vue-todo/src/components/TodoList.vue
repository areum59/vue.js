<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
                {{ todoItem }}
                <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">delete</span>
            </li>
            <!-- 에러가 나는 경우 v-for를 사용할 때 항상 v-bind:key를 사용해야 한다는 이유가 있는데
            vacode에서만 뜨는 에러로 무시해도 됨. (다른 에디터에서는 표시되지 않음) -->
        </ul>
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            todoItems: []
        }
    },
    methods: {
        removeTodo: function(todoItem, index){
            console.log(todoItem, index);
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        }
    },
    created: function(){
        if(localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++){
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    this.todoItems.push(localStorage.key(i));
                }
                // console.log(localStorage.key(i));
            }
        }
    }
};
</script>

<style scoped>
ul {list-style: none; padding-left: 0; margin-top: 0; text-align: left;}
ul li {display: flex; height: 50px; min-height: 50px; line-height: 50px; margin: 0.5rem 0; padding: 0 0.9rem; background-color: #fff; border-radius: 5px;}

.checkBtn {line-height: 45px; color: #62acde; margin-right: 5px;}
.checkBtnCompleted {color: #b3adad;}
.textCompleted {text-decoration: line-through; color: #b3adad;}
.removeBtn {margin-left: auto; color: #de4343; cursor: pointer;}
</style>