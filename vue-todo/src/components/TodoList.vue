<template>
    <div>
        <ul>
            <li v-for="todoItem in todoItems" v-bind:key="todoItem">
                {{ todoItem }}
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

</style>