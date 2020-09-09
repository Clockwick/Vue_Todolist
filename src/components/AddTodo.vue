<template>
  <div class="block">
      <input type="text" placeholder="Add Todos here .." v-model="title" required/>
      <button @click="addTodo" class="big-button" v-if="title.length">Add</button>
      <button @click="$emit('clear-all')" class="big-button">Clear all</button>
  </div>
</template>

<script>
import Vue from "vue";
import UUID from "vue-uuid";

Vue.use(UUID)
export default {
  name: 'AddTodo',
  props: ["todos"],
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id : this.$uuid.v4(),
        title: this.title,
        desp: "Simple detail",
        completed: false
      }
      this.$emit('add-todo', newTodo)
      this.title = ''
    },

  }
}
</script>

<style scoped>

  .block {
    display: flex;
    justify-content: center;
    margin-bottom: 3em;
    align-items: center;
  }
  input[type='text'] {
    height: 50px;
    font-size: 14pt;
    padding: 5px;
    margin-right: 30px;
  }
button {
  position: relative;
  display: inline-block;
  cursor: pointer;
  outline: none;
  border: 0;
  vertical-align: middle;
  text-decoration: none;
  font-size: 1.5rem;
  color:var(--colorShadeA);
  font-weight: 700;
  text-transform: uppercase;
  font-family: inherit;
  margin-bottom: 20px;
}

button.big-button {
   padding: 1em 2em;
   border: 2px solid var(--colorShadeA);
  border-radius: 1em;
  background: var(--colorShadeE);
transform-style: preserve-3d;
   transition: all 175ms cubic-bezier(0, 0, 1, 1);
}
button.big-button::before {
  position: absolute;
  content: '';
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--colorShadeC);
  border-radius: inherit;
    box-shadow: 0 0 0 2px var(--colorShadeB), 0 0.75em 0 0 var(--colorShadeA);
 transform: translate3d(0, 0.75em, -1em);
     transition: all 175ms cubic-bezier(0, 0, 1, 1);
}


button.big-button:hover {
  background: var(--colorShadeD);
  transform: translate(0, 0.375em);
}

button.big-button:hover::before {
  transform: translate3d(0, 0.75em, -1em);
}

button.big-button:active {
            transform: translate(0em, 0.75em);
}

button.big-button:active::before {
  transform: translate3d(0, 0, -1em);
  
      box-shadow: 0 0 0 2px var(--colorShadeB), 0 0.25em 0 0 var(--colorShadeB);

}


</style>

