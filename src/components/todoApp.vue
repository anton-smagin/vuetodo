<template>
  <div>
    <div class="row">
      <div v-if="loggedIn" class="login float-right">
        <logout/>
      </div>
      <div v-else>
        <login v-if="login"/>
        <signup v-else />
      </div>
    </div>
    <div v-if="!loggedIn" class="row">
      <div class="float-right">
        <button
          id="btn-or"
          class="btn btn-warning"
          v-on:click="login = !login"
        >
          or {{ login ? "sign up" : "login" }}
        </button>
       <div v-if="loggedIn" class="login float-right">
        <logout/>
        </div>
        <div v-else class="login float-right">
        <login v-if="login" />
        <signup v-else />
        <button
          id="btn-or"
          class="btn btn-warning  "
          v-on:click="login = !login"
        >
          or {{ login ? "sign up" : "login" }}
        </button>
      </div>
    </div>
    </div>
    <div class="row">
      <div class="col12 text-center">
        <div class="input-group">
          <input id="new-todo" type="text" placeholder="what your plan?" v-model="newTodo">
          <input id="new-image" type="text" placeholder="what's your img?" v-model="image">
          <button id="add-todo" class="btn" v-on:click="addToDo">Add ToDo</button>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col12">
        <ul  class="list-group" id="todos">
          <li v-for="(todo, index) in todos" v-bind:key="todo.id">
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
import axios from 'axios'

import todoItem from './todoItem.vue'
import signup from './signup.vue'
import login from './login.vue'
import logout from './logout.vue'

export default {
  components: {
    todoItem,
    signup: signup,
    login: login,
    logout: logout
  },
  data () {
    return {
      todos: [],
      newTodo: '',
      login: true,
      loggedIn: localStorage.getItem('token'),
      image: ''
    }
  },
  methods: {
    deleteToDo (id) {
      this.todos.splice(id, 1)
    },
    addToDo () {
      let vue = this
      axios
        .post(
          'https://gttodo.herokuapp.com/api/todos',
          { todo: { text: this.newTodo, image: this.image } },
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem('token')}`
            }
          })
        .then(function(response) {
          vue.todos.push(response.data)
          vue.newTodo = ''
        })
    },
    getTodos () {
      let vue = this
      axios
        .get('https://gttodo.herokuapp.com/api/todos',
        {
          headers:{
            Authorization: `Bearer ${localStorage.getItem('token')}`
          }
        })
        .then (function(response){
          vue.todos = response.data
        })
    },
  },
  mounted () {
    this.getTodos()
  },
}
</script>

<style>
  #new-todo {
    width: 50%;
  }
  .login {
    text-align: left;
    margin-bottom: 25px;
  }
  .login input{
    padding: 8px 10px;
  }
  .login .btn {
    padding: 10px;
  }

  #btn-or {
    padding: 10px;
  }
</style>
