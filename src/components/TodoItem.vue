<template>
    <div class="todo-item" :class="{ 'todo-item__done': isDone }">
      <input 
        v-if="!isEdit"
        class="todo-item__checkbox"
        type="checkbox" 
        :checked="isDone" 
        @change="onChange">
      <div v-if="!isEdit" class="todo-item__content">
        <span>{{ name }}</span>
        <span>{{ description }}</span>
      </div>
      <div v-if="isEdit" class="todo-item__input-container">
        <input v-model="updateTodo.name">
        <input v-model="updateTodo.description">
      </div>
      <div v-if="!isEdit" class="todo-item__btn-container">
        <button  
          :disabled="isDone"
          @click="editTodo"
        >&#9998;</button>
        <button 
          :disabled="isDone" 
          @click="deleteTodoFn(id)"
        >&#128465;</button>
      </div>
      <div v-if="isEdit" class="todo-item__btn-container">
        <button>&#10004;</button>
        <button @click="cancelEditTodo">&#10006;</button>
      </div>
    </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    name: String,
    description: String,
    isDone: Boolean,
    id: Number,
    checkedTodoFn: Function,
    deleteTodoFn: Function,
  },
  data() {
    return {
      isEdit: true,
      updateTodo: { name: this.name, description: this.description }
    }
  },
  methods: {
		onChange(e) {
			this.checkedTodoFn(this.id, e.target.checked);
		},
    editTodo() {
      this.isEdit = true;
    },
    cancelEditTodo() {
      this.isEdit = false;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .todo-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #d9dbda;
    margin: 6px 10px;
    padding: 6px;
    border-radius: 10px;
  }

  .todo-item__checkbox {
    flex-grow: 0.25;
    border: 1px solid #000;
  }

  .todo-item__content {
    display: flex;
    flex-grow: 3;
  }

  .todo-item__input-container {
    display: flex;
    justify-content: space-around;
    flex-grow: 6;
  }

  .todo-item__input-container input {
    width: 45%;
  }

  .todo-item__content span {
    padding: 0 6px;
  }

  .todo-item__btn-container {
    display: flex;
    justify-content: space-around;
    flex-grow: 0.5;
  }

  .todo-item__btn-container button {
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
    outline: none;
    border-radius: 50%;
    width: 20px;
    height: 20px;
  }

  .todo-item__done {
    background: #a3ffd1;
    color: #d9dbda;
  }
</style>
