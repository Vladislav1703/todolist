<template>
  <div id="app">
    <TodoList :todos="todos" @delete-todo="deleteTodo" @add-new-todo="addNewTodo" @change-todo="changeTodo" @toggle-checkbox="toggleCheckbox"></TodoList>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  data() {
    return {
      todos: [{description: 'посмотреть видео с папужкой', completed: true},
              {description: 'учёба', completed: false },
              {description: 'написание глупого списка', completed: false },
      ],
    }
  },
  components: {
    TodoList,
  },
  methods: {
    deleteTodo(index) { //удаляем задачу
      this.todos.splice(index, 1);
    },
    addNewTodo(text) { // добавляем задачу
      this.todos.push({description: text, completed: false})
    },
    changeTodo(index, text) { //если задачу изменяют -- значит она не выполнена
      this.todos[index] = {description: text, completed: false};
    }, 
    toggleCheckbox(boolean, index) {
      this.todos[index].completed = boolean;
    }
  }
}
</script>

<style>
  #app {
    background: linear-gradient(135deg, #00bfff 31%, #00bfff 0, #1e90ff 50%, #40cfff 0, #1e90ff 100%, #fff 0);
  }
</style>
