<template>
    <div class="todo-item" :class="{ 'todo-item__done': completed }">
      <input 
        v-if="!isEdit"
        class="todo-item__checkbox"
        type="checkbox" 
        :checked="completed" 
        @change="onChange">
      <div v-if="!isEdit" class="todo-item__content">
        <span>{{ title }}</span>
      </div>
      <div v-if="isEdit" class="todo-item__input-container">
        <input v-model="todo.title">
      </div>
      <div v-if="!isEdit" class="todo-item__btn-container">
        <button  
          :disabled="completed"
          @click="editTodo"
        >&#9998;</button>
        <button 
          :disabled="completed" 
          @click="deleteTodoFn(id)"
        >&#128465;</button>
      </div>
      <div v-if="isEdit" class="todo-item__btn-container">
        <button @click="updateTodo">&#10004;</button>
        <button @click="cancelEditTodo">&#10006;</button>
      </div>
    </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    title: String,
    completed: Boolean,
    id: Number,
    updateTodoFn: Function,
    deleteTodoFn: Function,
    checkedTodoFn: Function,
  },
  data() {
    return {
      isEdit: false,
      todo: { title: this.title }
    }
  },
  methods: {
		onChange(e) {
			this.checkedTodoFn(this.id, e.target.checked);
		},
    editTodo() {
      this.isEdit = true;
    },
    updateTodo() {
      this.updateTodoFn(this.id, this.todo);
      this.isEdit = false;
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
    width: 5%;
    border: 1px solid #000;
  }

  .todo-item__content {
    display: flex;
    width: 80%;
    overflow: hidden;
  }

  .todo-item__content span {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .todo-item__input-container {
    display: flex;
    justify-content: space-around;
    width: 85%;
  }

  .todo-item__input-container input {
    width: 100%;
  }

  .todo-item__content span {
    padding: 0 6px;
  }

  .todo-item__btn-container {
    display: flex;
    justify-content: space-around;
    width: 15%;
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
