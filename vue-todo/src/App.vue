<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <!-- v-on:="" 하위 컴포넌트에서 발생시킨 이벤트 이름="현재 컴포넌트의 methods 이름" -->
    <TodoList v-bind:propsdata="todoItems"></TodoList>
    <!-- v-bind="" 내려보낼 데이터 속성 이름="현재 위치의 컴포넌트" -->
    <TodoFooter></TodoFooter>
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
