<template>
  <app-header></app-header>
  <main>
    <add-todo v-on:AddNewTodo="AddTodo"></add-todo>
    <ul class="todos">
      <todo
        v-for="(item, i) in getTodo"
        :key="item.id"
        :todo="item"
        @dragstart="dragStart(i)"
        @Deleted="DeleteTodo"
        @changeStatus="changeTodoStatus"
        @dragover.prevent
        @drop="drop(i)"
      ></todo>
    </ul>
    <div class="card stat">
      <p class="corner">
        <span id="items-left">{{ getActiveTodoCount }}</span> مورد باقی مانده
      </p>
      <div class="filter">
        <button id="all" :class="{ on: activeTab == 'all' }" @click="changeTab('all')">همه</button>
        <button id="active" :class="{ on: activeTab == 'active' }" @click="changeTab('active')">
          فعال
        </button>
        <button
          id="completed"
          :class="{ on: activeTab == 'completed' }"
          @click="changeTab('completed')"
        >
          تکمیل
        </button>
      </div>
      <div class="corner">
        <button @click="deleteCompleted" id="clear-completed">حذف تکمیل شده ها</button>
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
      dragging: -1,
      activeTab: 'active'
    }
  },
  computed: {
    getActiveTodoCount() {
      return this.todos.filter((f) => f.isComplete == false).length
    },
    getTodo() {
      switch (this.activeTab) {
        case 'all':
          return this.todos
        case 'active':
          return this.todos.filter((f) => f.isComplete == false)
        case 'completed':
          return this.todos.filter((f) => f.isComplete == true)
        default:
          return this.todos
      }
    }
  },
  methods: {
    AddTodo(title) {
      const id = Math.random().toString(16).slice(2)
      const todo = { id, title, isComplete: false }
      this.todos.push(todo)
    },
    DeleteTodo(id) {
      this.todos = this.todos.filter((f) => f.id !== id)
    },
    changeTodoStatus(id, newStatus) {
      var newTodos = [...this.todos]
      var selectedTodo = newTodos.find((f) => f.id === id)
      selectedTodo.isComplete = newStatus
      this.todos = newTodos
    },
    deleteCompleted() {
      if (confirm('آیا از انجام عملیات اطمینان دارید ؟')) {
        var newTodos = [...this.todos]
        newTodos = newTodos.filter((f) => f.isComplete === false)
        this.todos = newTodos
      }
    },
    dragStart(index) {
      this.dragging = index
    },
    drop(index) {
      var newElement = this.todos.splice(this.dragging, 1)[0]
      this.todos.splice(index, 0, newElement)
    },
    changeTab(tab) {
      this.activeTab = tab
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
