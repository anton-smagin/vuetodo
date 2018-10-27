<template>
  <div>
    <div class="col5">
      <div class="input-group">
        <input id="new-todo" type="text" placeholder="what your plan?" v-model="newTodo">
        <button id="add-todo" class="btn" v-on:click="addToDo">Add ToDo</button>
      </div>
    </div>
    <div class="col5">
      <ul  class="list-group" id="todos">
        <li v-for="(todo, index) in todos" v-bind:key="todo + index">
          <todoItem
            v-bind:todo="todo"
            :todoindex="index"
            v-on:delete-todo="deleteToDo($event)"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import todoItem from './todoItem.vue'

export default {
  components: {
    todoItem
  },
  data () {
    return {
      todos: [],
      newTodo: ''
    }
  },
  methods: {
    deleteToDo (id) {
      this.todos.splice(id, 1);
    },
    addToDo () {
      this.todos.push(this.newTodo)
      this.newTodo = ''
    }
  },
}
</script>
