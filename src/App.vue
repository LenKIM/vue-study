<template>
  <div id="app">
    <!--    <TodoList v-bind:내려보낼 프롭스 속성 = "현재컴포넌트 데이터 속성"></TodoList>-->
    <!--    <TodoInput v-on:하위 컴포넌트에서 발생시킨 이름="현재컴포넌트의 메서드 명"></TodoInput>-->
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
<!--    <TodoList v-on:toggleItem="toggleOneItem"></TodoList>-->
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter";

export default {
  methods: {
    // addOneItem(todoItem) {
    //   const obj = {completed: false, item: todoItem};
    //   localStorage.setItem(todoItem, JSON.stringify(obj))
    //   this.todoItems.push(obj)
    // },
    // removeOneItem(todoItem, index) {
    //   localStorage.removeItem(todoItem.item)
    //   this.todoItems.splice(index, 1)
    // },
    // toggleOneItem(todoItem, index) {
    //   this.todoItems[index].completed = !this.todoItems[index].completed
    //   localStorage.removeItem(todoItem.item);
    //   localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
    // },
    // clearAllItems() {
    //   localStorage.clear();
    //   this.todoItems = [];
    // }
  },
  data() {
    return {
      todoItems: []
    }
  },
  components: {
    // '컴포넌티 이름': 컴포넌트 내용
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: wheat;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}

</style>