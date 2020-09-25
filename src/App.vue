<template>
  <div id="app">
    <NavBar title="ToDo"/>
    <TodoList 
      :todoList="todoList" 
      :addTodoFn="addTodo" 
      :updateTodoFn="updateTodo"
      :deleteTodoFn="deleteTodo"
      :checkedTodoFn="checkedTodo"
    />
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    TodoList,
  },
  data() {
    return {
      todoList: [
        { 
          id: Date.UTC(2020, 9, 21), 
          name: 'One', 
          description: 'One todo',
          isDone: false,
        },
        { 
          id: Date.UTC(2020, 9, 22),
          name: 'Two', 
          description: 'Two todo',
          isDone: true,
        }
      ],
    }
  },
  methods: {
    addTodo(todo) {
      this.todoList = [
        ...this.todoList,
        { id: Date.now(), isDone: false, ...todo }
      ];
    },
    updateTodo(id, todo) {
      this.todoList = this.todoList.map(el => el.id === id ? { ...el, ...todo } : el);
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter(el => el.id !== id);
    },
    checkedTodo(id, isDone) {
      this.todoList = this.todoList.map(el => el.id === id ? { ...el, isDone } : el);
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: calc(100vh - 90px);
}
</style>
