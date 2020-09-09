<template>
    <div>
      <md-divider />
      <div class="block">
          <div class="topic" v-bind:class="{'is-completed': todo.completed}">
            <div class="input">
              <md-checkbox v-model="todo.completed"></md-checkbox>
            </div>
            <h3 class="title">
              {{todo.title}}
            </h3>
          </div>
          <md-icon class="del" @click.native="$emit('del-todo', todo.id)">remove_circle</md-icon> 
      </div>
      <md-divider />
    </div>
      
  <!--<div class="todo-item" v-bind:class="{'is-completed': todo.completed}">

  <h2>
    <input type="checkbox" v-on:change="markCompleted" /> {{todo.title}}
    <button class="del" @click="$emit('del-todo', todo.id)">x</button>
  </h2>
  </div>
  -->
</template>

<script>

export default {
  name: 'TodoItem',
  props: ["todo"],
}

</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #000 solid;
  text-align: center;
}
.is-completed {
  text-decoration: line-through;
}
.block {
  display: flex;
  padding: 10px;
}
.topic {
  display: flex;
}
.del {
  margin: auto 10px;
}
.del:hover {
  color: red;

}

</style>
