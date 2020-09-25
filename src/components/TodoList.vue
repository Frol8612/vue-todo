<template>
  <div class="todo-list">
    <div class="todo-list__form">
      <input v-model="newTodo.name" placeholder="name" />
      <input v-model="newTodo.description" placeholder="Description" />
      <button @click="addTodo">&#10010;</button>
    </div>
    <div class="todo-list__container">
      <TodoItem 
        v-for="item in todoList" 
        :key="item.name"
        :name="item.name" 
        :description="item.description"
        :isDone="item.isDone"
        :id="item.id" 
        :checkedTodoFn="checkedTodoFn"
        :deleteTodoFn="deleteTodoFn"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  props: {
    todoList: Array,
    addTodoFn: Function,
    deleteTodoFn: Function,
    checkedTodoFn: Function,
  },
  data() {
    return {
      newTodo: {
        name: '',
        description: '',
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.name && this.newTodo.description) {
        this.addTodoFn(this.newTodo);
        this.newTodo = { name: '', description: '' };
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .todo-list {
    display: flex;
    flex-direction: column;
    height: 100%;
    padding: 16px 6px; 
  }

  .todo-list__form {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 50%;
    padding: 6px 10px;
  }

  .todo-list__form input {
    position: relative;
    padding: 3px 6px;
    border: none;
    outline: none;
    margin-right: 10px;
    border-bottom: 1px solid #000;
  }

  .todo-list__form input:nth-child(1) {
    flex-grow:  1;
  }

  .todo-list__form input:nth-child(2) {
    flex-grow:  2;
  }

  .todo-list__form button {
    border: none;
    outline: none;
    border-radius: 50%;
    min-width: 25px;
    height: 25px;
    box-shadow: 0 0 5px 0 #000;
  }

  .todo-list__form button:active {
    box-shadow: 0 0 1px 0 #000;
  }

  .todo-list__container {
    margin-top: 16px;
    width: 50%;
    min-width: 400px;
  }
</style>
