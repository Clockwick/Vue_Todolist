<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in sortedArray">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue"
export default {
  name: 'Todos',
  props: ["todos"],
  computed: {
    sortedArray: function() {
      return this._.orderBy(this.todos, ['completed', false])
    }
  },
  components: {
    TodoItem
  },
}
</script>

