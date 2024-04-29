<template>
  <div class="container">
    <h1>Simple Todo App</h1>
    <div class="todo-input-container">
      <input type="text" v-model="newTodo" class="todo-input" @keyup.enter="addTodo">
      <button class="todo-button" @click="addTodo">Add</button>
    </div>

    <ul>
      <li v-for="(todo, index) in todos" :key="index" class="todo-item" :data-index="index">
        <input type="checkbox" v-model="todo.completed" class="todo-checkbox">
        <span :class="{ 'completed': todo.completed }" class="todo-text" @click="toggleCompletion(todo)">
          {{ todo.text }}
        </span>
        <button class="todo-delete" @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: ''
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false });
        this.newTodo = '';
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleCompletion(todo) {
      todo.completed = !todo.completed;
      const todoTextElement = document.querySelector('.todo-item[data-index="' + this.todos.indexOf(todo) + '"] .todo-text');
      if (todo.completed) {
        todoTextElement.classList.add('completed');
      } else {
        todoTextElement.classList.remove('completed');
      }
    }
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 500px;
  margin: 20px auto;
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #333;
  margin-bottom: 20px;
}

.todo-input {
  width: calc(100% - 80px);
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  margin-right: 10px;
  font-size: 16px;
}

.todo-button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background-color: #4ca3af;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}

.todo-button:hover {
  background-color: #5ab4e9;
}

ul {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  color: #4ca3af;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #eeeeee;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-text {
  flex-grow: 1;
  cursor: pointer;
}

.todo-delete {
  background-color: #1900f7;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  margin-left: 10px;
  cursor: pointer;
}

.todo-delete:hover {
  background-color: #ee11dc;
}

.todo-text.completed {
  color: rgb(0, 17, 255);
  text-decoration: line-through; /* New: Add line-through decoration */
}
</style>