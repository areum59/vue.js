<template>
    <div>
        <ul>
            <!-- v-for를 사용할 때 에러가 나는 경우 : 항상 v-bind:key를 사용해야 한다는 이유가 있는데
            vacode에서만 뜨는 에러로 무시해도 됨. (다른 에디터에서는 표시되지 않음) -->
            <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
                <!-- check 버튼 -->
                <span class="checkBtn" v-on:click="toggleComplete(todoItem, index)" 
                    v-bind:class="{checkBtnCompleted: todoItem.completed}">
                    <font-awesome-icon icon="fas fa-check" />
                </span>

                <!-- list -->
                <span v-bind:class="{textCompleted: todoItem.completed}">
                    {{ todoItem.item }}
                </span>

                <!-- list 삭제 버튼 -->
                <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                    <font-awesome-icon icon="fas fa-trash-alt" />
                </span>
            </li>
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
            // splice() : 배열의 삭제 또는 교체하거나 새 요소를 추가
        },
        toggleComplete: function(todoItem, index){
            console.log(todoItem, index)
            todoItem.completed = !todoItem.completed;
            // 바뀐 설정값을 저장하기 위해서는 새로운 정보로 업데이트하는 속성이 없기때문에 removeItem()으로 지운 후 동일하게 세팅하여 바뀐내용을 저장
            // 즉, 로컬 스토리지의 데이터를 갱신하는 DOM
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        }
    },
    created: function(){
        if(localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++){
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                    // .parse() : string을 오브젝트로 변경
                }
            }
        }
    }
};
</script>

<style scoped>
ul {list-style: none; padding-left: 0; margin-top: 0; text-align: left;}
ul li {display: flex; height: 50px; min-height: 50px; line-height: 50px; margin: 0.5rem 0; padding: 0 0.9rem; background-color: #fff; border-radius: 5px;}

.checkBtn {line-height: 45px; color: #62acde; margin-right: 8px;}
.checkBtnCompleted {color: #b3adad;}

.textCompleted {text-decoration: line-through; color: #b3adad;}

.removeBtn {margin-left: auto; color: #de4343; cursor: pointer;}
</style>