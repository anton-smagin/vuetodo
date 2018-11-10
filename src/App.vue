<template>
    <div class="container">
    <div class="row" id="header">
      <div class="col">
        <h1 class="text-center">My todo list</h1>
      </div>
    </div>
    <div class="row">
      <div id="app">
        <todoApp/>
      </div>
    </div>
  </div>
</template>

<script>
import todoApp from './components/todoApp.vue'

export default {
  name: 'app',
  components: {
    todoApp
  }
}
</script>

<style>
#app, #header {
  padding: 20px;
  background-color: #efefef;
}

#app {
  height: 100vh;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
.text-center {
  text-align: center;
}

.float-right {
  text-align: right;
  margin-left: auto;
}

.row {
  clear: both;
  width: 100%;
}

.col6 {
  width: 50%;
  float: left;
}

.col12 {
  width: 100%;
  float: left;
}

.btn {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
}

.btn-danger {
  background-color: #f44336;
}

.btn-warning {
  background-color: #b7b95c;
}

input, li, .btn {
  padding: 14px 28px;
  font-size: 16px;
}

li {
  align-items: center;
  list-style-type: none;
  background-color: #f9f9f9;
}

.list-group-item {
  display: flex;
}

.todo-text {
  font-size: 20px;
}
</style>
