<template>
<div>
  <div v-if="editing" class="edit-todo list-group-item">
    <div class="input-group">
      <input id="edit-todo" class="col6" type="text" v-model="text">
      <div class="btn-group float-right">
        <button
          v-on:click="saveToDo()"
          class="btn btn-success"
          id="save-todo"
        >
          save ToDo
        </button>
      </div>
    </div>
  </div>
  <div class="list-group-item" v-else>
    <div class="row">
    <span class="todo-text">
      {{text}}
    </span>
    <div class="btn-group btn-group-sm float-right" role="group">
      <button class="btn btn-warning todo-edit" v-on:click="editToDo()">edit</button>
      <button class="btn btn-danger todo-delete" v-on:click="deleteToDo()">delete</button>
    </div>
    </div>
    <div class="row">
      <img :src="image" width=100 height=100>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['todo', 'todoindex'],
  data () {
  return {
    editing: false,
    text: this.todo.text,
    id: this.todo.id,
    image: this.todo.image,
  }
},
  methods: {
    saveToDo () {
      let vue = this
      axios
        .put(
          this.todoPath(),
          { todo: { text: this.text } },
          { headers: { Authorization: `Bearer ${localStorage.getItem('token')}` } }
        )
        .then(function(response) {
          vue.text = response.data.text
          vue.editing = false
        })
    },
    editToDo () {
      this.editing = true
    },
    deleteToDo () {
      let vue = this
      axios
        .delete(
          this.todoPath(),
          { headers: { Authorization: `Bearer ${localStorage.getItem('token')}` } }
        )
        .then(function() {
          vue.$emit('delete-todo', vue.todoindex)
        })
    },
    todoPath() {
      return `https://gttodo.herokuapp.com/api/todos/${this.id}`
    }
  }
}
</script>

<style>
  .input-group {
    width: 100%;
  }
</style>
