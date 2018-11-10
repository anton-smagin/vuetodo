<template>
  <div>
    <div class="row">
      <div class="col12 text-center">
        <div class="input-group">
          <input id="new-todo" type="text" placeholder="what your plan?" v-model="newTodo">
          <button id="add-todo" class="btn" v-on:click="addToDo">Add ToDo</button>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col12">
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

<style>
  #new-todo {
    width: 50%;
  }
</style>
