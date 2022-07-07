<template>
  <div id="app">
    <TodoHeader />
    <TodoInput v-on:addTodo="addTodo" />
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo" />
    <TodoFooter v-on:removeAll="clearAll" />
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "app",
  data() {
    return {
      todoItems: []
    };
  },

  methods: {
    addTodo(todoItems) {
      localStorage.setItem(todoItems, todoItems);
      this.todoItems.push(todoItems);
    },

    removeTodo(todoItems, index) {
      localStorage.removeItem(todoItems);
      this.todoItems.splice(index, 1);
    },

    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    }
  },

  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) != "loglevel:webpack-dev-server") {
          this.todoItems.push(localStorage.key(i));
          // 스토리지에있는(배열형태) index를 매개로 값을 todoItem[] 에 push()
        }
      }
    }
  },

  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter
  }
};
</script>

<style>
body {
  text-align: center;
  background-color: darkgrey;
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
