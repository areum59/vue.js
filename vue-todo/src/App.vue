<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!-- v-on:="" 하위 컴포넌트에서 발생시킨 이벤트 이름="현재 컴포넌트의 메서드 이름" -->
    <!-- v-bind="" 내려보낼 데이터 속성 이름="현재 위치의 컴포넌트" -->
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  name: 'App',
  data: function(){
    return{
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(todoItem){
      var obj = {completed: false, item: todoItem};
      // check box에 진입을 했는지 체크함.
      localStorage.setItem(todoItem, JSON.stringify(obj));
      // .stringify() : 오브젝트를 string로 변환
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index){
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
      // splice() : 배열의 삭제 또는 교체하거나 새 요소를 추가
    },
    toggleOneItem: function(todoItem, index){
      this.todoItems[index].completed = !this.todoItems[index].completed
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      // 바뀐 설정값을 저장하기 위해서는 새로운 정보로 업데이트하는 속성이 없기때문에
      // removeItem()으로 지운 후 동일하게 세팅하여 바뀐내용을 저장
      // 즉, 로컬 스토리지의 데이터를 갱신
    },
    clearAllItems: function(){
      localStorage.clear();
      // .clear() : 로컬스토리지에 있는 모든 내용을 지우는 API
      this.todoItems = [];
    }
  },
  created: function(){
    if(localStorage.length > 0) {
      for(var i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  components: {
    // '컴포넌트 태그명' : 컴포넌트 내용
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }
}
</script>

<style>
body {text-align: center; background-color: #f8f8f8;}
input {border-style: groove; width: 200px;}
button {border-style: groove;}

.shadow {box-shadow: 2px px 10px rgba(0,0,0,0.3);}
</style>
