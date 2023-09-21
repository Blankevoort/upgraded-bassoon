<template>
  <app-header></app-header>
  <main>
    <add-todo v-on:AddNewTodo="AddTodo"></add-todo>
    <ul class="todos">
      <todo
        v-for="(item, index) in todos"
        :key="item.id"
        :todo="item"
        @Deleted="deleteTodo"
        @changeStatus="changeTodoStatus"
        @dragstart="dragStart(index)"
        @dragover.prevent
        @drop="dropOn(index)"
      ></todo>
    </ul>
    <div class="card stat">
      <p class="corner"><span id="items-left">0</span> مورد باقی مانده</p>
      <div class="filter">
        <button id="all" class="on">همه</button>
        <button id="active">فعال</button>
        <button id="completed">تکمیل</button>
      </div>
      <div class="corner">
        <button id="clear-completed" @click="deleteCompleted">حذف تکمیل شده ها</button>
      </div>
    </div>
  </main>
  <app-footer></app-footer>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import AddTodo from './components/AddTodo.vue'
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  components: { AppHeader, AppFooter, AddTodo, Todo },
  data() {
    return {
      todos: [],
      dragging: -1
    }
  },
  methods: {
    AddTodo(title) {
      const id = Math.random().toString(16).slice(2)
      const todo = { id, title, isComplete: false }
      this.todos.push(todo)
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((f) => f.id !== id)
    },
    changeTodoStatus(id, status) {
      var newTodo = [...this.todos]
      var selectedTodo = newTodo.find((f) => f.id === id)
      selectedTodo.isComplete = status
      this.todos = newTodo
    },
    deleteCompleted() {
      if (confirm('آیا از حذف کارهای اتمام یافته خود اطمینان دارید؟')) {
        var newTodo = [...this.todos]
        newTodo = newTodo.filter((f) => f.isComplete == false)
        this.todos = newTodo
      }
    },
    dragStart(index) {
      this.dragging = index
    },
    dropOn(index) {
      var newElement = this.todos.splice(this.dragging, 1)[0]
      this.todos.splice(index, 0, newElement)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
