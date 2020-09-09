<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo" v-bind:todos="todos" v-on:clear-all="clearTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-if="todos.length" />
    <h1 v-else>Nothing left today ! ! !</h1>
  </div>
</template>

<script>
import Vue from 'vue'
import VueLodash from 'vue-lodash'
import lodash from 'lodash'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'

import Todos from './components/Todos.vue'
import Header from './components/layout/Header.vue'
import AddTodo from './components/AddTodo.vue'

Vue.use(VueMaterial)
Vue.use(VueLodash, { name: 'custom' , lodash: lodash })

const STORAGE_KEY = 'todo-storage'

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: [],
    }
  },
  created() {
    this.todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos))
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos))
    },
    clearTodo() {
      this.todos = []
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos))
    },
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
} 
h1 {
  text-align: center;
}

:root {
  --backgroundColor: rgba(246, 241, 209);
  --colorShadeA: rgb(106, 163, 137);
  --colorShadeB: rgb(121, 186, 156);
  --colorShadeC: rgb(150, 232, 195);
  --colorShadeD: rgb(187, 232, 211);
  --colorShadeE: rgb(205, 255, 232);
}
</style>
